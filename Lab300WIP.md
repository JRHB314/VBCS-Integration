
<details><summary>2. Connect VBCS to the Firebase Database</summary>
  
<h3> Create New Page </h3>
  
First thing we want to do is create another page, this one called book-catalog, on which we will display our book descriptions and images. Right click on main-start and hit `Duplicate`, then right click on the copy to rename it `book-catalog`. On the Design view of the page, click on the "Welcome to the Home Page" heading, then hit the trash can icon in the bottom left of the right bar to delete the component.<br>
![](/images/3-25.png)<br>
<br>
Now we have to update the tab bar to include this new page. Go to the code view for the page and look for the "oj-tab-bar-XXXXXXXXX-X" item. Inside that you should see two oj-tab-bar-XXXXXXXXX-X-tab-X items. Copy the code for the first tab (the one with dull formatting) and paste it right below the code for the second tab. Rename the tab "Catalog" and change the listener to clickCatalogTab (though this event does not yet exist. Finally, change the first tab's style to bright, so only the third tab is dull.<br>
![](/images/3-26.png)<br>
<br>
Repeat this process for the other pages, but on the other pages, the Catalog tab should have bright styling. <br>
![](/images/3-27.png)<br>
<br>  
Now we just need to create our action chain navigateCatalogPage (created at the flow level) and our event clickCatalogTab (created for each page) and we are good to go. Double check that you can navigate between all three pages.<br>
  
  <h3> Add HTML/CSS </h3>
  
  Now that our database has been set up, we'll need to connect it to VBCS. We'll be using this database information to populate one of our pages with images and descriptions of books, so the first thing we need to do is to come up with a layout of how we want our page to look. For this lab, we'll format the page with a left-side column to display book images and a right-side column to display the book information.<br>
  
  Let's create this layout by adding the HTML structure to our new book-catalog page. Navigate to the `Code` view of the page, and copy and paste this HTML code and add it at the very end:<br>

  ```
  <div class="row">
     <div class="column"> <div id="leftColumn"></div> </div>
     <div class="column"> <div id="rightColumn"></div> </div>
</div>
  ```
  <br>
  
  With the HTML in place, we can next add the css for the two columns to style them properly:
  
  ```
    .column {
      float: left;
      width: 35%;
  }

  .row:after {
      content: "";
      display: table;
      clear: both;
  }
  ```
  ![](/images/3-d1.png)<br>
  <br>
  
  With these 2 div objects properly set up, we'll be able to identify where the javascript should populate the images and descriptions. Let's move on to the actual Javascript.<br>
  
  <h3> Add the Javascript </h3>
  
VBCS requires that functions be written in a very particular way. You will see the base outline for this already here.<br>

![](/images/3-14.png)<br>
<br>

The outermost function will return a PageModule object to VBCS; it sends all of the module functions we create to VBCS so we can more easily access them in other components. Each module can be treated like a separate Javascript file.<br>

To define a module, use this format:
```
PageModule.prototype.functionName = function () { OUR CODE HERE };
```
Our functions will look like:
```
define([], function() {
  'use strict';

  var PageModule = function PageModule() {};
  PageModule.prototype.functionOne = function () { OUR CODE HERE };
  PageModule.prototype.functionTwo = function () { OUR CODE HERE };
  PageModule.prototype.functionThree = function () { OUR CODE HERE };

  return PageModule;
});
```
To get started, let's set up the module that will load the book descriptions. <br>
```
define([], function() {
  'use strict';

  var PageModule = function PageModule() {};
  
  PageModule.prototype.loadDescriptions = function () {
    //code here
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

<h3>Calling the Module Function.</h3>

We want this function to be called whenever the page loads. Go to `Events` on the left sidebar for the Catalog page.<br>
Click `Create Event Listener`, then under `Lifecycle Events`, select `vbEnter`. This will be an event that runs whenever the page loads.<br>
![](/images/3-15.png)<br>
<br>
Hit the + sign next to Page Action Chains to create a new action chain. Name this runLoadDescriptions.<br>
![](/images/3-16.png)<br>
<br>
Click on the name of your event, then on the right side hit the link to open the action chain editor.<br>
![](/images/3-17.png)<br>
<br>
Drag "Call Module Function" onto the plus sign.<br>
![](/images/3-18.png)<br>
<br>
Select Module Function. You should see a Page Function named loadDescriptions in the list. Select it, and you should be good to go.<br>
![](/images/3-19.png)<br>
<br>
Test the page, and the books should appear on the {pagename} page. <br>
![](/images/3-20.png)<br>
<br>
Now we are going to create our other module, loadImages. The process is basically the same, except we are appending images instead of text.<br>
Insert this code alongside the first module:
```
  PageModule.prototype.loadImages = function() {
    const app = document.getElementById('leftColumn');

    var request = new XMLHttpRequest();
    request.open('GET', 'https://asset-bdf37.firebaseio.com/results.json', true);

    request.onload = function () {
      // Begin accessing JSON data here
      var data = JSON.parse(this.response);
      if (request.status >= 200 && request.status < 400) {
        Object.keys(data).forEach(result => {
          const bookCovers = document.createElement('img');
          bookCovers.src = data[result].image_url;
          console.log(result);
          app.appendChild(bookCovers);
          const p = document.createElement('p');
          p.textContent = "\n";
          app.appendChild(p);
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
Add another action change under vbEnter, this one called `runLoadImages`. Set it up the same as runLoadDescriptions, with this one calling the loadImages module.<br>
<br>
Test the page one more time, and we should see the book covers to the left of the book descriptions. <br>
![](/images/3-21.png)<br>
<br>
Great job!
  
</details>
