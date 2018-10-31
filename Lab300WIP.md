<h2> Lab 300: Connecting VBCS to a Firebase database </h2>

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
<h3>Calling ther Module Function.</h3>
We want this function to be called on page load. Go to Events for the {pageName} page.<br>
Click Create Event Listener, then under Lifecycle Events, hit the plus by vbEnter. This will be an event that runs when the page loads.<br>
{image}<br>
<br>
Click on the name of your event, then on the right side hit the link to open the action chain editor.<br>
{image}<br>
<br>
Drag "Call Module Function" onto the plus sign.<br>
{image}<br>
<br>
Select Module Function. You should see a Page Function named loadDescriptions in the list. Select it, and you should be good to go.<br>
{image}<br>
<br>
Test the page, and the books should appear on the {pagename} page. <br>
{image}<br>
<br>

