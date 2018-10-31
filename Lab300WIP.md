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

<details><summary>2b. Show Books on Website</summary>

<h3> Show Books on Website </h3>

Within the OUR CODE section, we will simply put in our javascript the way we would if we were creating a javascript file to run. Ours will actually have another function within it, making this a function within a function within a function within a function. <br>
First, let's set up the module that will load the book descriptions. <br>
```
define([], function() {
  'use strict';

  var PageModule = function PageModule() {
    PageModule.prototype.loadDescriptions = function () {
      //code here
    };
  };

  return PageModule;
});
```
Then we want to grab the rightcolumn so that we can append elements to that part of the page. Put this in the "code here" section.
```
const app = document.getElementById('rightColumn');
```
Now we are ready to make our GET request to our database. Make sure to replace the url below with the url for your database.
```
var request = new XMLHttpRequest();
request.open('GET', 'https://projectname-XXXXXX.firebaseio.com/books.json', true);
```
We want to peform some actions once this request is made.
```
request.onload = function () {
  //actions to perform once request is made
}
```
Before we can do anything with the response, we have to parse it as a JSON. Put this code inside the request.onload function.
```
var data = JSON.parse(this.response);
```
Right below that, put this code. It will run desired actions if the request is a success, and return an error if there's a problem.
```
if (request.status >= 200 && request.status < 400) {
  //actions to perform on successful request
}
else {
  const errorMessage = document.createElement('marquee');
  errorMessage.textContent = "Request failed.";
  app.appendChild(errorMessage);
}
```
Next we are going to run through the children of the JSON response and add each entry as a line on our webpage. We'll also add a horizontal rule between each, and use a blank image to add some space between book descriptions.
```
        if (request.status >= 200 && request.status < 400) {
          Object.keys(data).forEach(result => {
            const line = document.createElement('hr');
            app.appendChild(line);
            
            const title = document.createElement('p');
            title.textContent = data[result].title;
            app.appendChild(title);
            const author = document.createElement('p');
            author.textContent = data[result].author;
            app.appendChild(author);
            const ISBN = document.createElement('p');
            ISBN.textContent = result;
            app.appendChild(ISBN);
            const genre = document.createElement('p');
            genre.textContent = data[result].genre;
            app.appendChild(genre);
            const published = document.createElement('p');
            published.textContent = data[result].publish_date;
            app.appendChild(published);
            const publisher = document.createElement('p');
            publisher.textContent = data[result].publisher;
            app.appendChild(publisher);
            
            const space = document.createElement('img');
            space.src = "https://i.imgur.com/gAYM6Ws.png?3";
            app.appendChild(space);
          });
        }
```
Finally, all together:
```
PageModule.prototype.loadDescriptions = function () {
            
      const app = document.getElementById('rightColumn');      

      var request = new XMLHttpRequest();
      request.open('GET', 'https://asset-bdf37.firebaseio.com/results.json', true);

      request.onload = function () {
        // Begin accessing JSON data here
        var data = JSON.parse(this.response);
        if (request.status >= 200 && request.status < 400) {
          Object.keys(data).forEach(result => {
            const line = document.createElement('hr');
            app.appendChild(line);
            
            const title = document.createElement('p');
            title.textContent = data[result].title;
            app.appendChild(title);
            const author = document.createElement('p');
            author.textContent = data[result].author;
            app.appendChild(author);
            const ISBN = document.createElement('p');
            ISBN.textContent = result;
            app.appendChild(ISBN);
            const genre = document.createElement('p');
            genre.textContent = data[result].genre;
            app.appendChild(genre);
            const published = document.createElement('p');
            published.textContent = data[result].publish_date;
            app.appendChild(published);
            const publisher = document.createElement('p');
            publisher.textContent = data[result].publisher;
            app.appendChild(publisher);
            
            const space = document.createElement('img');
            space.src = "https://i.imgur.com/gAYM6Ws.png?3";
            app.appendChild(space);
          });
        }
        else {
          const errorMessage = document.createElement('marquee');
          errorMessage.textContent = "Request failed.";
          app.appendChild(errorMessage);
        }
      }

      request.send();
    };
```
Careful with your brackets here; it's easy to get one too many or one too few. <br>
Last step is calling this function on page load.
Go to Events on the last side. 
Click Create Event Listener, then under Lifecycle Events, hit the plus by vbEnter. This will be an event that runs when the page loads.
Click on the name of your event, then on the right side hit the link to open the action chain editor.
Drag Call Module Function onto the plus sign.
Select Module Function. You should see a Page Function named [name] in the list. Select it, and you should be good to go.
Test the page, and the books should appear. 

