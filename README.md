

<h2> Lab 400: Connecting VBCS to a Graph Database (Neo4j) </h2>

In this part of the lab, we'll learn a bit about how Graph Databases work, and see how to integrate them with VBCS. Specifically, we'll be using a free Graph Database called Neo4j.

<details>
  <summary>1. Set up the Neo4j Database </summary>
  
  <h3>Create the Neo4j Database </h3>
  
  Visit [Graphene DB](https://app.graphenedb.com/) and sign up for an account. Login to the dashboard, then click `Create Database`.
  
  ![](/images/david-gdb-1.png)<br>
<br>
  
  Select the free "Sandbox" tier.<br>
  
  ![](/images/david-gdb-2.png)<br>
<br>

  Give your database a name. Leave the default Neo4j Version as 3.4.9 and click `Create Database`.<br>

  ![](/images/david-gdb-3.png)<br>
<br>

  On the next page, a pop up should appear asking you to create a user. Click `Create user now`.<br>
  
  ![](/images/david-gdb-4.png)<br>
<br>

  Give your user a Label with no expiration date and click `Create User`.<br>
  
  ![](/images/david-gdb-5.png)<br>
<br>

  <b>Copy down your credentials. This is the only time you'll be able to see the password, so make a note of it.</b><br>
  
  ![](/images/david-gdb-6.png)<br>
<br>

  <h3>Populate the Database </h3>
  
  Under the main dashboard's Overview tab, under the Tools section, hit `Launch`. This will open a Neo4j Browser in another tab.<br>
  
  ![](/images/david-gdb-7.png)<br>
<br>

  On the top section of the page, we can write console commands to begin populating our database.<br>

  ![](/images/david-gdb-8.png)<br>
<br>

  Now that we have succesfully created our graph database as well as a user for it, we can learn a bit more on how they work.<br>
  
</details>

<details>
  <summary>2. <b>(Optional)</b> Getting Familiar with Graph Databases </summary><br>
  
  <b>Note</b>: You can skip this section and jump to the next if you are already know how graph databases work.<br>

  In graph databases, there are `Nodes` and `Relationships`. Neo4j uses a language called Cypher to interact with its databases, rather than the SQL statements of relational databases. Nodes are enclosed in parantheses to resemble circles, and relationships are described using arrows. For this example, we'll create a database of users, where each user can "follow" another user (think Instagram). Copy and paste this Cypher statement in the top console bar:
  
  ```
  CREATE (userA:Person {name:"A"}) 
  CREATE (userB:Person {name:"B"}) 
  CREATE (userA)-[rel:FOLLOWS]->(userB) 
  return userA, userB, rel
  ```
  <b>Explanation</b>: In this code snippet, we are creating two users, referenced by userA and userB, of type "Person", with an attribute called "name". After we have the two nodes created, we create a relationship referenced by "rel" of type "FOLLOWS" between userA and userB. Notice that all nodes have a unique ID field (similar to primary keys in the relational database model).<br>
  
  ![](/images/david-gdb-10.png)<br>
<br>
  
  With 2 nodes and a relationship successfully created, let's create a 3rd node and relationship. Enter the following code snippet in the console:
  
  ```
  CREATE (userC:Person {name:"C"})
  CREATE (userA)-[rel:FOLLOWS]->(userC)
  return userA, userC, rel
  ```
  
  ![](/images/david-gdb-11.png)<br>
<br>
  
  Uh oh, it looks like the A node showed up blank. Why is that? We created userA in the previous Cypher statement, but because we are writing a separate Cypher statement, it has no idea how to reference that userA. That is, the references we create to nodes only last one statement, and can be changed in the next; "userA" is not stored as a property of "A". We could call it "N", "nodeA", or whatver we want, and it only has to be consistent within the query. <br>
  
  Now we have to first find A and C since we just created them using `MATCH`. This is similar to a SELECT statement in SQL, and this allows us to use "userA" and "userC" as references.
  
```
  MATCH (userA:Person {name:"A"})
  MATCH (userC:Person {name:"C"})
  CREATE (userA)-[rel:FOLLOWS]->(userC)
  return userA, userC, rel
```

  ![](/images/david-gdb-12.png)<br>
<br>

  Great! A is now properly following C.<br>
  
However, if we run `MATCH (n) RETURN (n)` to return all nodes, we'll see that there's still that empty node following C: 

![](/images/david-gdb-13.png)<br>
<br>

To get rid of it, hover over the invisible node, grab its id and run `MATCH (n) where id(n) = # DETACH DELETE n` where # is the ID of the node.<br>

![](/images/david-gdb-14.png)<br>
<br>

Also note that `MATCH (n) RETURN (n)` simply returns all nodes; it doesn't <i>technically</i> return their relationships. The Graph visualizer will show these relationships anyway, but the JSON returned (look at the `Table` tab) does not. To return all nodes and their relationships, run `MATCH (n)-[r]->(m) RETURN n,r,m;`.

![](/images/david-gdb-15.png)<br>
<br>
  
Great! Everything looks correct. Now let's say that we want userC to be followed by 5 other users. We could create 5 followers and then define their relationship with userC, but the easier approach would be to use a `FOREACH` loop:
  
  ```
  MATCH (userC:Person {name:"C"})
  FOREACH (followerName in ["follower1","follower2","follower3","follower4","follower5"] |
    CREATE (:Person {name: followerName})-[:FOLLOWS]->(userC))
  ```
  
  Your graph should look like:<br>
  
  ![](/images/david-gdb-16.png)<br>
<br>
  
  Notice that here in the relationship, we don't need to write `[rel:FOLLOWS]` because we are simply creating the relationship, and don't reference it later in the query.<br>
  
  If we want to view who follows userC:
  
  ```
  MATCH (cFollowers)-[:FOLLOWS]->(userC:Person {name:"C"})
  RETURN cFollowers
  ```
  
  ![](/images/david-gdb-17.png)<br>
<br>
  
  Now that we've had a little practice with Neo4j and graph databases, let's jump into creating the actual data we'll use to mimic our "Instagram model". We need a clean start, so let's reset the database with:

  ```
    MATCH (n) OPTIONAL MATCH (n)-[r]-() DELETE n,r
  ```
  
</details>

<details>
  <summary>3. Populating Our Graph Database </summary><br>
  <h3>Populating Our Graph Database</h3>
  
  Let's create a user named Rachel Webb. Then, let's create some people that follow her:
  
  ```
  CREATE (userA:Person {name:"RachelWebb"})
  FOREACH (followerName in ["SamArcher", "AprilGold", "JacqueNoir", "BradHillman", "JaneDoe", "AngelinaGibbs",   "YukiTsukino","JohanLitwick","VelmaGarcia","PamelaSelzer"] |
  CREATE (:Person {name:followerName})-[:FOLLOWS]->(userA))
  ```
  
  View all the current nodes/relationships: `MATCH (n)-[r]->(m) RETURN n,r,m;`.<br>
  
  ![](/images/david-gdb-18.png)<br>
<br>
  
  Now that we have a person named Rachel Webb along with some people that follower her, let's give her followers their own followers: 
  
  ```
  MATCH (userB:Person {name:"SamArcher"})
  FOREACH (userName in ["BradHillman", "BobFlinstone", "JaneDoe"] |
  MERGE (userID:Person {name:userName})
  CREATE (userID)-[:FOLLOWS]->(userB))
  ```
  
  Verify that your graph looks like this:<br>
  
 ![](/images/david-gdb-19.png)<br>
<br> 
  
  We just gave Sam Archer 3 followers. In this code snippet, we use `MERGE` instead of `CREATE` since we want to either create a relationship for an existing node, or, if our node doesn't yet exist, create it. userID is an arbitrary reference we give to the creation of these new nodes when using the `MERGE` function. Remember, these references can be named anything we want; these names were chosen to be easy to understand.<br>
  
  Let's continue to add followers. Go to the resources folder, copy and paste the code in "CreateFollowers" into the browser console and run it.<br> 
  
  ![](/images/david-gdb-21.png)<br>
<br> 
  
  At this point your graph probably looks a bit messy, but your graph should resemble something like this:<br>
  
  ![](/images/david-gdb-20.png)<br>
<br> 
  
<br>
  Let's take a moment to review a few things. First of all, the large chunk of code that we just placed had a line that said:<br>
  
  ```
  WITH count(*) as dummy
  ```
  
  What is this? This line simply allows us to run multiple Cypher commands at once. Cypher doesn't like to run unrelated queries; the `WITH` statement links the queries together, but essentially does nothing. Think of this as a workaround to make it easier to share the code.<br>
  
  Here's another thing to note. In the code that we just pasted, take a close look at userE:<br>
  
  ```
  MATCH (userE:Person {name:"MariaGomez"})
  FOREACH (userName in ["JacqueNoir"] |
    MERGE (userID:Person {name:userName})
    CREATE (userID)-[:FOLLOWS]->(userE))
  ```
  
 Maria wasn't created as one of Rachel's followers. However, she still exists by this point. This is because the `MERGE` command created her as one of Jacque's followers. That's the power of MERGE--it won't create a duplicate, but it will create an element if it doesn't exist. <br>
 
  Also note that there is no command for userH (BobFlinstone). Bob has no followers, so we don't need to create any. Poor Bob.<br>
  
  Next, we'll want to add a little more detail to these users. We'll add a profile picture and a quote for each user. Again, go to the resources folder in this directory, this time copying and pasting the code from the AddInformation file.<br>
  
  ![](/images/david-gdb-22.png)<br>
<br>
  
  Each statement follows this basic format:
  
```
MATCH (n:Person {name:'UserName'}) 
SET n.image = 'https://some-image-url.jpg'
SET n.quotes = 'Here is a really meaningful quote!'
```

First we MATCH "n" to the node with name "UserName". Then we use SET to add these two new fields. The AddInformation file runs a bunch of these Cypher statements for each respective user.<br>

  Phew! And we're done. To recap, we added a Person named Rachel Webb, gave her followers, and then added some more followers to Rachel Webb's followers through our createFollowers resource. Then, we added two more attributes to each person: their image URL, and a quote that they display. Awesome!
  
</details>

<details>
<summary>4. Showing User Info on VBCS </summary><br>
  <h3>Showing User Info</h3>
  
  Let's go ahead and create an entirely new web app, as this lab does not relate to our Library website. Click the computer icon on the far left, then hit the plus sign next to Web Apps. Name it whatever you like.<br>
<br>
The first thing to do is drag and drop an Input Text component into the top left of the page. Change the label to be one column big by clicking on it, then draging the little box on the edge. Change its text to say "Search Name". Move over the text field to be right next to the label, and change it to be two columns wide. To the right of that, drag on a button, and have it say "Search". <br>
![](/images/4-10.png)<br>
<br>
In the next row, drag a Panel. By default, it fills the page horizontally, but this isn't what we want. We also can't drag the component to resize it the way we can most components. Go to the Code view and find the `oj-panel` div. You'll see something that says "oj-sm-12 oj-md-12". These indicate the how many columns the component should take up for "small" and "medium" views of the page. For this we will be working with medium screens, so change oj-md to oj-md-5. <br>
![](/images/4-11.png)<br>
<br>
Inside the panel, at the very left, drag on a Heading component. Drag the slider bar under the General tab so that it is only H4. Call this "Username".<br>
![](/images/4-12.png)<br>
<br>
Now let's add a picture. This will be the searched user's profile picture. Drag and drop an Image component into the left side of the panel underneath Username. Drag an edge so it becomes four columns wide. In the General tab on the right, set width and height to 100. Next to the image we want to have three rows, so drag on a Flex Container object. Make sure it is only three columns wide. Drag and drop three Text components inside this container so that they are stack vertically. Name the first "Followers:", the second "Following:", and the third "Mutuals:". <br>
![](/images/4-13.png)<br>
<br>
To the left of these, we want to have three more Text components that will be filled with the follower, following, and mutual counts. Drag and drop another Flex Container to the right of the first, and add three Text components, each named "count". We will replace these with variables in a moment. Below the image, drag and drop one last Text component. Fill in "quote" for this field.<br>
![](/images/4-14.png)<br>
<br>
Keep in mind, if you lose track of a component or have trouble clicking on something to customize it, you can open up the Page Structure.<br>
![](/images/4-15.png)<br>
<br>
Click the icon again to close it.<br>
<br>
Next we need to create some String variables to be bound to our components.<br>
-searchUsername: the username that will be searched. Put this in the Data field for the topmost Text field. <br>
-username: the returned username. Set it's default value to "Username." Put this variable in place of the "Username" heading we had before.<br>
-imageURL: will hold the returned source image url. Set the default value to `https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/Pictogram_voting_question.svg/220px-Pictogram_voting_question.svg.png`. Then put this for the source url of the Image component.<br>
-followerCount: will hold the returned follower count. Put this in the Data field of the top "count" text.<br>
-followingCount: will hold the returned following count. Put this in the Data field of the middle "count" text.<br>
-mutualCount: will hold the returned mutuals count. Put this in the Data field of the bottom "count" text.<br>
-favoriteQuote: will hold the returned quote. Put this in the Data field of the "Quote" text. Set default value to "Favorite Quote".
![](/images/4-16.png)<br>
![](/images/4-17.png)<br>
Note that "count"s disappeared. Since those variables don't have a default value, they start out as empty Strings.<br>
<br>
We are ready to set up our Service Connection. In Lab 300 we called the REST endpoint in our Javascript, but VBCS actually offers a nice feature to make REST calls without (much) coding. On the far left, hit the icon that looks like a wire with a bump in it (the third from the top) and then hit the plus sign to create a new Service Connection. Choose Define by Endpoint.<br>
![](/images/4-18.png)<br>
<br>
Now, we need our REST endpoint URL. Reopen your GrapheneDB Database, and go to the Connection tab. There you will find your HTTP REST endpoint.<br>
![](/images/4-19.png)<br>
<br>
Copy and paste that URL on VBCS, then add `/transaction/commit` to the end of it. Change Method to POST. <br>
![](/images/4-20.png)<br>
<br>
Hit next. Change Service Name to "Neo4j Get User Data". <br>
![](/images/4-21.png)<br>
<br>
Go to the Authentication tab, and choose `Basic` from the dropdown. You should have already made a database user in GrapheneDB; if not, review part 1 of this lab. Enter in the username and password for this user. <b>This is not the same as your GrapheneDB account.</b> <br>
![](/images/4-22.png)<br>
<br>
On the Request tab, copy and paste this code:
```
{
  "statements" : [ {
    "statement" : "MATCH (n:Person {name:'YukiTsukino'}) return n"
  } ]
}
```
This will simply return the node and all of its information. We'll select the specific fields we want in VBCS later. <br>
Note; it is just an example. We will not be searching for YukiTsukino every time. <br>
<br>
Finally, on the Test tab scroll down slightly until you see the `Send` button. <br>
The response should look like this:
```
{
    "results": [
        {
            "columns": [
                "n"
            ],
            "data": [
                {
                    "row": [
                        {
                            "image": "https://inhabitat.com/wp-content/blogs.dir/1/files/2013/12/snowflake10.jpg",
                            "name": "YukiTsukino",
                            "quotes": "If youre reading this... Congratulations, youre alive. If thats not something to smile about, then I dont know what is."
                        }
                    ],
                    "meta": [
                        {
                            "id": 33,
                            "type": "node",
                            "deleted": false
                        }
                    ]
                }
            ]
        }
    ],
    "errors": []
}
```
In the top right of the response, hit `Copy to Response Body`. Now hit Create.<br>

<br>This means we are ready to set up an Action Chain. Back on our web page, click the search button to go to its Events tab; hit `New Event`, then `QuickStart: click`. <br>
![](/images/4-22.5.png)<br>
<br>
Drag a Call REST Endpoint action onto the plus sign in the chain, then click `Select Endpoint`.<br>
![](/images/4-23.png)<br>
<br>
Expand `Service Connections` and select the endpoint we just created. <br>
![](/images/4-24.png)<br>
<br>
Note, the service connection above has a slightly different name than the one suggested. This should not make a difference.<br>
<br>
Now we are going to append three string variables to create the request body. The first and last variables do not change; they are the main part of the request. The middle string is the searchUsername we already made. By appending all three we can change out which user we are searching for. <br>
Go back to the main page's variables. Create two Strings, getDataPt1 and getDataPt2. <br>
For getDataPt1, set this default value: `{  "statements": [   {    "statement": "MATCH (user:Person {name:  '`<br>
For getDataPt2, set this default value: `'}) return user"   }  ] }`<br>
Together with the searchUsername, it will be <br>
`{  "statements": [   {    "statement": "MATCH (user:Person {name: 'searchUsername'}) return user"   }  ] }`. <br>
<br>
Go back to the action chain. Click on the REST Call action, and then click on the body paramater. <br>
![](/images/4-25.png)<br>
<br>
Drag getDataPt1, then searchUsername, then getDataPt2, onto body. <br>
![](/images/4-26.png)<br>
<br>
Great! The request should be correctly formatted. Now, to display the response, we need to do one more action. Drag a Assign Variables action onto the next step in the chain, then hit `Assign` next to `Variables`. <br>
On the left, expand callRestEndpoint1 -> body -> results -> item[0] -> data -> item[o] -> row -> item[0], until it looks like this:<br>
![](/images/4-27.png)<br>
<br>
Drag `image` on the left to `imageURL` on the right, `name` on the left to `username` on the left, and `quotes` on the left to `favoriteQuote` on the right. Then hit `Save`. <br>
![](/images/4-28.png)<br>
<br>
Test your website! Enter in AprilGold for the username, then hit search. You should see this:<br>
![](/images/4-29.png)<br>
<br>

  
</details>
