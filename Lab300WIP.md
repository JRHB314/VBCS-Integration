<h2> Lab 300: Connecting VBCS to a Firebase database </h2>
  
  
<details><summary>1. Set up a Firebase Realtime Database</summary>
  
<h3> Set up a Firebase Database </h3>

Go to the [Firebase Website](https://firebase.google.com/products) and select Realtime Database.<br>
![](/images/3-1.png)<br>
<br>
Click "Visit Console" then "Add Project".
![](/images/3-2.png)<br>
![](/images/3-3.png)<br>
<br>å
Choose a name, leave the default settings for location, make sure all three boxes are checked, then hit Create Project.<br>
![](/images/3-4.png)<br>
<br>
It will take 10 seconds or so to create, then the page should redirect you to your Database home page. Note that currently, there is no data in our database.<br>
![](/images/3-5.png)<br>
<br>
First thing we need to do is edit the security rules to allow read write access. Since this is just a test database, it doesn't need to be secure. Go to the Rules tab and simply change read and write to "true". For a real project, you would want more specific rules. Google has documentation on how to create more complex rules [here](https://firebase.google.com/docs/database/security). <br>
![](/images/3-12.png)<br>
<br>
Now, inside this GitHub repository, navigate to the "resources" directory and download the bookList.json file. Open it inside VCode or your preferred text editor. Note the structure is of several book objects identified by ISBN. <br>
![](/images/3-6.png)<br>
<br>
Go back to the Data tab of your Database. Near the top right, hit the three dots dropdown, then "Import JSON".<br>
![](/images/3-7.png)<br>
<br>
Import the bookList.json file.<br>
![](/images/3-8.png)<br>
<br>
Your database should populate with the information from the file.<br>
![](/images/3-9.png)<br>
<br>
To test that everything is set up correctly, enter the shown url for the Database /books.json into a browser.<br>
![](/images/3-10.png)<br>
```
https://projectname-XXXXX.firebaseio.com/books.json
```
A list of the books and all their info should be shown. <br>
![](/images/3-11.png)<br>
<br>
Sidenote, if you do not already have the extension JSON Viewer or something similar, I recommend adding it to your browser.

</details>


