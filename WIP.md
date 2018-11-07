# Set up page to show relationships

Now, we want to list the Follower, Following, and Mutual users when the corresponding word on the page is clicked. First, however, we have to do some more page set up. <br>
Create two variables:
-title, which will hold the heading for our list
-relationsList, which will hold the returned list
On page designer, drag and drop a Heading component below the panel, and set its Text value to `title`. Right below that, drag and drop a Paragraph component. Make it only one column wide. This will force the line to wrap, so that each listed user appears on a new line. Set its Text value to `relationsList`. <br>
![](/images/400/4-40.png)<br>
<br>
Next we need three onClick listeners for our three labels. Create three action chains, called `loadFollowers`, `loadFollowing`, and `loadMutuals`. Leave them blank for right now. <br>
![](/images/400/4-41.png)<br>
<br>
Similarly, create three Other Events, `followersClick`, `followingClick`, and `mutualsClick`. Select their corresponding action chain.<br>
![](/images/400/4-42.png)<br>
<br>
First, to make it more obvious that the words are clickable, we are going to style them. Go to the Code view of the page and insert this code at the top:
```
<style>

.clickableText {
color: #35e3ed;
text-decoration: underline;
cursor: pointer;
}

</style>
```
We set the color to a nice aqua; underline it; and have the cursor turn into a pointer when it hovers over the text.<br>
<br>
The HTML for the three words will have to be replaced; simply surrounding the oj-bind-text in a div class will not work here. Instead we'll turn it into plain text surround by our clickableText div class.<br>
![](/images/400/4-43.png)<br>
<br>
Back on Design view:<br>
![](/images/400/4-44.png)<br>
<br>

# rels listed


