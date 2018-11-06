<h2> Lab 400: Part something something setting up on VBCS  </h2>

Let's go ahead and create an entirely new web app, as this lab does not relate to our Library website. Click the computer icon on the far left, then hit the plus sign next to Web Apps. Name it whatever you like.<br>
{img}
<br>
The first thing to do is drag and drop an Input Text component into the top left of the page. Change the label to be one column big by clicking on it, then draging the little box on the edge. Change its text to say "Search Name". Move over the text field to be right next to the label, and change it to be two columns wide. To the right of that, drag on a button, and have it say "Search". <br>
{img}
<br>
In the next row, drag a Panel. By default, it fills the page horizontally, but this isn't what we want. We also can't drag the component to resize it the way we can most components. Go to the Code view and find the `oj-panel` div. You'll see something that says "oj-sm-12 oj-md-12". These indicate the how many columns the component should take up for "small" and "medium" views of the page. For this we will be working with medium screens, so change oj-md to oj-md-5. <br>
{img}
<br>
Inside the panel, at the very left, drag on a Heading component. Drag the slider bar under the General tab so that it is only H4. Call this "Username".
{img}
<br>
Now let's add a picture. This will be the searched user's profile picture. Drag and drop an Image component into the left side of the panel underneath Username. Drag an edge so it becomes four columns wide. In the General tab on the right, set width and height to 100. Next to the image we want to have three rows, so drag on a Flex Container object. Make sure it is only three columns wide. Drag and drop three Text components inside this container so that they are stack vertically. Name the first "Followers:", the second "Following:", and the third "Mutuals:". <br>
{img}
<br>
To the left of these, we want to have three more Text components that will be filled with the follower, following, and mutual counts. Drag and drop another Flex Container to the right of the first, and add three Text components, each named "count". We will replace these with variables in a moment. Below the image, drag and drop one last Text component. Fill in "quote" for this field.<br>
{img}
<br>
Keep in mind, if you lose track of a component or have trouble clicking on something to customize it, you can open up the Page Structure.<br>
{img}
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
{img}
{img}
<br>
This means we are ready to set up our Service Connection. In Lab 300 we called the REST endpoint in our Javascript, but VBCS actually offers a nice feature to make REST calls without (much) coding. On the far left, hit the icon that looks like a wire with a bump in it (the third from the top) and then hit the plus sign to create a new Service Connection. Choose Define by Endpoint.<br>
{img}
<br>
Now, we need our REST endpoint URL. Reopen your GrapheneDB Database, and go to the Connection tab. There you will find your HTTP REST endpoint.<br>
{img}
<br>
Copy and paste that URL on VBCS, then add `/transaction/commit` to the end of it. Change Method to POST. <br>
{img}
<br>
Hit next. Change Service Name to "Neo4j Get User Data". <br>
{img}
<br>
Go to the Authentication tab, and choose `Basic` from the dropdown. You should have already made a database user in GrapheneDB; if not, review part 1 of this lab. Enter in the username and password for this user. <b>This is not the same as your GrapheneDB account.</b> <br>
{img}
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

<br>This means we are ready to set up an Action Chain. Back on our web page, click the button to go to its Events tab; hit `New Event`, then `QuickStart: click`. Drag a Call REST Endpoint action onto the plus sign in the chain, then click `Select Endpoint`.<br>
{img}
<br>
Expand `Service Connections` and select the endpoint we just created. <br>
{img}
<br>
Now we are going to append three string variables to create the request body. The first and last variables do not change; they are the main part of the request. The middle string is the searchUsername we already made. By appending all three we can change out which user we are searching for. <br>
Go back to the main page's variables. Create two Strings, getDataPt1 and getDataPt2. <br>
For getDataPt1, set this default value: `{  "statements": [   {    "statement": "MATCH (user:Person {name:  '`<br>
For getDataPt2, set this default value: `'}) return user"   }  ] }`<br>
Together with the searchUsername, it will be `{  "statements": [   {    "statement": "MATCH (user:Person {name: 'searchusername'}) return user"   }  ] }`. <br>
Go back to the action chain. Click on the REST Call action, and then click on the body paramater. <br>
{img}
<br>
Drag getDataPt1, then searchUsername, then getDataPt2, onto body. <br>
{img}
<br>
Great! The request should be correctly formatted. Now, to display the response, we need to do one more action. Drag a Assign Variables action onto the next step in the chain, then hit `Assign` next to `Variables`. <br>
On the left, expand callRestEndpoint1 -> body -> results -> item[0] -> data -> item[o] -> row -> item[0], until it looks like this:<br>
{img}
<br>
Drag `image` on the left to `imageURL` on the right, `name` on the left to `username` on the left, and `quotes` on the left to `favoriteQuote` on the right. Then hit `Save`. <br>
{img}
<br>
Test your website! Enter in AprilGold for the username, then hit search. You should see this:<br>
{img}
<br>

<br>

## Next part idk

Now we want to be able to return a) the count of followers/following/mutuals and b) the list of followers/following/mutuals. <br>
Let's start with the count. We're going to have to make another Service Connection, even though we are using the same URL, because our request and response bodies will be formatted differently. Make a new Service Connection, copy and paste your Database REST endpoint URL /transaction/commit into the URL, set method to POST, and hit next. <br>
{img}
<br>
Name it Neo4j Relations Count and set up Authentication the same way as before. <br>
{img} {img}
<br>
As mentioned, our request will be a bit different:
```
{
  "statements" : [ {
    "statement" : "MATCH (user:Person {name:'YukiTsukino'}) RETURN size((user)-->()) as out, size((user)<--()) as in"
  } ]
}
```
Go to Test and hit Send. The response should look like this:
```
{
    "results": [
        {
            "columns": [
                "out",
                "in"
            ],
            "data": [
                {
                    "row": [
                        4,
                        2
                    ],
                    "meta": [
                        null,
                        null
                    ]
                }
            ]
        }
    ],
    "errors": []
}
```
Finally, hit Copy to Response Body, and you're done with the connection.<br>
{img}
<br>

# Break

Now we will add another two variables to our page `relCountPt1` and `relCountPt2`. <br>
relCountPt1: `{  "statements": [   {    "statement": "MATCH (user:Person {name: '`<br>
relCountPt2: `'}) RETURN size((user)<--()) as in, size((user)-->()) as out, size((user)-->()-->(user)) as mutuals"   }  ] } `<br>
Again, searchUsername will go in the middle. You can see that the Cypher statement is returning three things: ingoing relationships (followers of user), outgoing relationships (people who the user is following), and people who the the user follows, that also follow the user (mutual follow). <br>
Go to our ButtonClickAction, and drag and drop a Call REST Endpoint action. Choose the `Neo4j Realtionship Count` connection we just made.<br>
{img}
<br>
Body:<br>
{img}
<br>
Drag and drop an Assign Variables action. <br>
Assign followerCount with a simple drag and drop like so:<br>
{img}
<br> 
However, you'll notice it only lists the first element in the returned row. For followingCount and mutualCount, we need the second and third elements respectively. Go ahead and drag `item[0]` over to following count, but change the `row[0]` to be `row[1]`. <br>
{img}
<br> 
Do the same thing for mutualCount, but this time chaging `row[0]` to be `row[2]`. <br>
{img}
<br> 
