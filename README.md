# VBCS Integration

<h2> Lab 100: Starting Your Web App </h2>

This lab will guide you through creating your first Web App in VBCS. 
  
<details>
  <summary>1. Create The Web App</summary>

  <h3> Create Web App </h3> 

  Sign in to your Cloud Account. <br>
  ![](/images/1.png) <br>
  ![](/images/2.png) <br>
  <br>

  Navigate to Cloud Dashboard, then open the Visual Builder Service Console. If Visual Builder is not visible, click `Customize Dashboard`, then scroll to Visual Builder in the list and hit `Show`.<br>

  ![](/images/3.png) <br> <br>

  At the top right of the page, hit "Quick Starts". This will allow us to create the underlying infrastructure for VBCS at the same time that we create the VBCS instance rather than making them separately. Simply name the instance and then hit `Create`. If you don't care about configuring the database that your instance will run on, this is the way to go. 

  Alternatively, you can hit the `Customize` button on the top right. This would allow you to configure the database that is created. For the purpose of this lab, we'll stick to the default QuickStart configuration.

  ![](/images/5.png)<br><br>

  Next, download the generated SSH key and credentials in order to continue, which will allow you to access your instance.

  <br>![](/images/12.png)<br>
  <br>

  Your instance will take some time to provision. When it's ready, open the Visual Builder Home page.

  <br>![](/images/8.png)<br>
  <br>

  Now, we need to create a Visual Application. From the home page, hit `New` in the top right. 

  <br>![](/images/9.png)<br>
  <br>

  Name the application whatever you like; the Description is optional. 

  <br>![](/images/10.png)<br>
  <br>

  Your new Application should open automatically. On the left, hit the computer icon for `Web Apps`, then the plus sign to create a new Web App. Name it, then hit `Create`. 

  <br>![](/images/11.png)<br>
  <br>

  A blank page will open in the center, with a Components Bar to the left and a Customization Bar on the right.<br>
  
  ![](/images/14.png)<br>
  <br>
</details>

<details>
  <summary>2. Customize Web App</summary>
  
  <h3>Customize Web App </h3>
  
  Click on the `Design` view tab in the top right. Drag on an image component into the very top left corner of the page.<br>
  Click on it, then look on the right side go to the Data tab. Put in `https://png.icons8.com/color/1600/reflector-bulb.png` 
  for the source url. This image will act as our website's logo.<br> 
  
  As it is, the image size is bigger than what we'd expect for our logo, so let's resize it. 
  
  <br>![](/images/15.png)<br><br>
  
  Go to the `General` tab and set the `width` property to 150. Now that the image is resized, it looks much more fitting to be   our website's logo.<br>
  
  ![](/images/16.png)<br>
  <br>
  
  Next, drag on a `Heading` component one column to the right of the logo. Under the `General` tab inside the `Text` field,   
  enter whatever name you'd like your website to be called.<br>
  
  In the row below, drag over a tab bar. The tab bar defaults to three tabs, but we only need two for now. Hover over `Tab 3`   in the General tab, then hit the trash can icon. Rename the tabs `Home` and `Second Page`.<br>
  
  ![](/images/17.png)<br>
  ![](/images/1-17.5.png)<br>
  
  Drag and drop another Heading component, and fill in "Welcome to the Home page" for the text.<br>
  
  Let's say that we want to customize the color of the text that we just entered. Click on the Heading, go to the `All` 
  tab, then expand `General Attributes` and scroll down to the `Style` field. Enter in `color: #67aee5;`. The color 
  changes to a light blue. This is an easy way to customize the CSS for a specific component. <br>
  
  ![](/images/1-18.png)<br>
  <br>
  
  In addition, we can also edit the HTML and CSS code directly. Near the top right, hit the `Code` view for the page. <br>
  
  ![](/images/1-19.png)<br><br>
  
  To customize the tab bar, we'll first define some style. Simply paste this at the top of the Code page.<br>
  
  ```
  <style>
  .bright {
  background-color: #4286f4;
  border-style: groove;
  }
  .dull {
  background-color: #7790ba;
  border-style: groove;
  }
  </style>
  ```
  
  <br>
  We will add this style as div classes to our tabs, with dull being for the tab we are currently on, and bright being for 
  tabs we are not on.<br>

  ![](/images/1-20.png)<br><br>
  
  Back on the design tab, we can view changes we made to the tab bar. As demonstrated, you can code HTML and CSS for your web   app the way you would for any website, while also having the option to change it in the Design view, giving you much greater flexibility.<br>
  
  ![](/images/1-21.png)<br>
  <br>
  
 </details>
  
<details>
  <summary>3. Add Navigation</summary>

  <h3>Add Navigation </h3>

  In order for this tab bar to actually navigate the website, we need a second page to navigate <i>to</i>. We want to carry over the components from the first page to this home page (logo, title, navbar) so we'll go ahead and copy it. Go to the Web App heirarchy on the left, right click on main-start and hit `Duplicate`. Then rename the page `second-page`.<br>
  ![](/images/1-33.png)<br>
  <br>
  
  Switch which tab is dull and which tab is bright. Dull tabs represent the current page we're on. <br><br>
  ![](/images/1-23.png)<br>
  <br>
  
  On the Design view, change "Welcome to the Home Page" to say "Welcome to the Second Page". It should look like this.<br>
  ![](/images/1-24.png)<br>
  <br>
  
  Next, let's create some <i>events</i> and <i>action chains</i>. These will allow us to navigate to the second page and back 
  again whenever a specific tab is clicked, rather than the text itself.<br>
  
  Click on flow `main`, and hit the flag icon near the left to open up `Actions`. Creating an action chain at the flow level 
  allows us to reuse these components on each page.<br>
  
  ![](/images/25.png)<br>
  <br>
  
  Hit `+ Action Chain` to create a new action chain and call it something like `navigateHome`. <br>
  Drag and drop a Navigate component to the plus sign, then click `Select Target`.<br>
  
  ![](/images/26.png)<br>
  <br>
 
  Choose `Peer Page`, and then `main-start`.<br>
  
  ![](/images/27.png)<br>
  ![](/images/28.png)<br>
  <br>
  
  Repeat this process for a navigateSecondPage action chain, this time selecting second-page as target.<br>
  <br>
  
  Events need to be created at the page level, because the event that triggers your action happens on a particular page. Go     back to main-start and click on the bell icon near the left to go to Events. Hit `+ Event Listener`.
  
  ![](/images/29.png)<br>
  <br>
  
  Scroll down to "Other Events" and hit the plus sign. Call this something like `clickHomeTab`. When done, hit `Select`.<br>
  
  ![](/images/30.png)<br>
  <br>
  
  On the next page, select `navigateHome` for the action chain, then hit `Select`.<br>
  ![](/images/31.png)<br>
  <br>
  
  Repeat this process for creating cxckSecondTab and having it trigger navigateSecondPage.<br>
  Then, create these same events for second-page.<br>
  
  ![](/images/32.png)<br>
  <br>
  
  Last but not least, we want to connect these event listeners to be activated whenever our tabs are clicked. Go to Code view,   and add the onclick listener after the lid for both tabs. Enter
  
  ```
  <li id ="oj-tab-bar-XXXXXXXXX-X-tab-X" on-click="[[$listeners.eventName]]"
  ``` 
  
  where eventName is the name of your event for each tab (i.e., clickHomeTab and clickSecondTab). <br>
  
  ![](/images/1-34.png)<br>
  <br>
  
  Note that many components have an Events tab that allows you to create an event and action chain all in one click, but    
  because we want different parts of the tab bar to take us to different pages, we have to set them up manually.<br>
  The Events tab is very useful for things such as buttons, where you can quickly create an action for when the button is 
  clicked.<br><br>
  
  Finally, add the onclick listeners for the second page, and you should be good to go! You now have a functional website.<br>
  <br>
  
  Click on the play button in the top right to test your website, seeing that you can navigate between the two pages.<br>
  
  ![](/images/1-7.png)<br>
  <br>
</details>

<h2> Lab 200: Connecting VBCS to an Oracle Database </h2>

Oracle offers quick tools to integrate Oracle Cloud Databases with VBCS.

<h2> Lab 300: Connecting VBCS to a Firebase Database </h2>

Now we will try connecting to a non-Oracle Cloud Database; in this case, Google's Firebase. 
  
<details>
  <summary>1. Set up a Firebase Realtime Database</summary>
  
  <h3> Set up a Firebase Database </h3>

  Login to a google account and go to the [Firebase Website](https://firebase.google.com/products). Select Realtime Database.<br>
  ![](/images/3-1.png)<br>
  <br>
  Click "Visit Console" then "Add Project".
  ![](/images/3-2.png)<br>
  ![](/images/3-3.png)<br>
  <br>
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

  Sidenote: If the formatting of your data looks different, add the JSON Viewer extension to your Chrome browser: https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh?hl=en-US.

</details>

<details>
  <summary>2. Connect VBCS to the Firebase Database</summary>
  
<h3> Create New Page </h3>
  
First thing we want to do is create another page, this one called book-catalog, on which we will display our book descriptions and images. Right click on main-start and hit `Duplicate`, then right click on the copy to rename it `book-catalog`. On the Design view of the page, click on the "Welcome to the Home Page" heading, then hit the trash can icon in the bottom left of the right bar to delete the component.<br>
![](/images/3-25.png)<br>
<br>
Now we have to update the tab bar to include this new page. Go to the code view for the page and look for the "oj-tab-bar-XXXXXXXXX-X" item. Inside that you should see two oj-tab-bar-XXXXXXXXX-X-tab-X items. Copy the code for the first tab (the one with dull formatting) and paste it right below the code for the second tab. Rename the tab "Catalog" and change the listener to clickCatalogTab (though this event does not yet exist. Finally, change the first tab's style to bright, so only the third tab is dull.<br>
![](/images/3-26.png)<br>
<br>
You could have gone to customize the tab bar on the Design view and hit the plus sign to the right of the title `Tabs` in the customization bar, but this would not have copied the style or the listener.<br>
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
Test the page, and the books should appear on the Catalog page. <br>
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

<details>
  <summary>3. Creating a Search Page </summary>
  
  <h3> Creating the Website's Search Functionality </h3>
  
  Let's review what we've done until this point. So far, we've built our web application, created a Firebase database and populated it with information, and wrote custom Javascript to extract data from our database URL. We invoked those functions and had them run at page load time, and we were able to display book images and descriptions on our catalog page. Great! But what if we want to display books based on a user search? That takes a bit of extra work. We'll need to first capture the user's input, and then parse our JSON object accordingly.<br>
  
  First create a third page for this website's search functionality. We'll call it "search". Duplicate `main-start` and rename the copy `search`.<br> 
Change "Welcome to the Home page." to say "Search". Drag and drop a `user input` box for the user to type in their search term, followed by a `button` for running that search. Click on the `Input Text` label and change it to say "Genre:". Let's also drag over a button to the right of the input text. Change the text of the button to "search".<br> 
 
 ![](/images/3-ds3.png)<br>
<br>

Note, however, that we only have three tabs; we need to make one more tab for the new page.<br>
Briefly,<br>
-Copy and paste code for a new tab in each page.<br>
-Change the tab name to "Search" and the onclick listener to clickSearchTab.<br>
-Create an action chain navigateSearchPage at the flow level.<br>
-Create an event listener on each page called clickSearchTab.<br>
Review Step 2. if you want more specific instructions. 

 ![](/images/3-30.png)<br>
<br>
 
  Now that we've finished our simple layout, we need to save the user's input into a variable. On the left side click the (x) icon to open up `Variables` page. Create a new variable and call it "genre".<br>
 
 ![](/images/david-search-5.png)<br>
<br>
 
 Go back to the search page and click on the text input box. Under `Data`, enter `{{ $page.variables.genre }}`. This saves the value that the user types into our genre variable.
 
 ![](/images/david-search-6.png)<br>
<br>
 
 Next, let's copy over the Javascript code. Under the `JS` tab of our catalog page, copy and paste the two slightly modified functions below onto our search page. 
 
 ```
   PageModule.prototype.loadDescriptions = function (inputGenre) { // our function now takes in a "genre" input

        const app = document.getElementById('rightColumn');      

        var request = new XMLHttpRequest();
        request.open('GET', 'https://asset-bdf37.firebaseio.com/results.json', true);

        request.onload = function () {
          // Begin accessing JSON data here
          var data = JSON.parse(this.response);
          if (request.status >= 200 && request.status < 400) {
            Object.keys(data).forEach(result => {     
              if(data[result].genre == inputGenre){ // we'll only want to display descriptions for a specific genre
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
              }
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
 
 ```
   PageModule.prototype.loadImages = function(inputGenre) { // our function now takes in a "genre" input
        const app = document.getElementById('leftColumn');

        var request = new XMLHttpRequest();
        request.open('GET', 'https://asset-bdf37.firebaseio.com/results.json', true);

        request.onload = function () {
          // Begin accessing JSON data here
          var data = JSON.parse(this.response);
          if (request.status >= 200 && request.status < 400) {
            Object.keys(data).forEach(result => {
              if(data[result].genre == inputGenre){ // we'll only want to display images for a specific genre
                const bookCovers = document.createElement('img');
                bookCovers.src = data[result].image_url;
                console.log(result);
                app.appendChild(bookCovers);
                const p = document.createElement('p');
                p.textContent = "\n";
                app.appendChild(p);
              }
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
 
 ![](/images/david-search-7.png)<br>
<br>
 
 Now that we have our logic, let's bind this logic to an action. Under Designer view, click the Search button. Under the `Events` tab, click `New Event -> Quick Start Click`. 
 
 ![](/images/david-search-8.png)<br>
<br>
 
 An action chain window has popped up. Drag over a `Call Module Function`. Click `Select Module Function`. Under "Page Functions", select our `loadImages` function.<br>
 
 ![](/images/david-search-9.png)<br>
<br>

Recall that our function now takes in a paramter, so on the right side under `Input Paramters`, map `inputGenre` to our `Genre` variable. Click `save`.<br> 

![](/images/david-search-10.png)<br>
<br>

 Now perform the same steps for the `loadDescriptions` function (drag another module function in for the loadDescriptions function, and bind the paramters to the function). The end action chain should look like this: <br>

 ![](/images/david-search-11.png)<br>
<br>

 Let's test our page out. Click the `Live` button at the top right corner. Enter in `Fantasy` and hit search. Our website now loads all the books with the fantasy genre! <i>(If the search button displays at the bottom of the page instead of the top, re-order the left-column and right-column HTML divs to the end of your page HTML code).</i>
 
 ![](/images/3-ds12.png)<br>
<br>
 
Try hitting the search button again. Uh oh, looks like the page is getting populated with the same books every time someone hits search. 

![](/images/david-search-13.png)<br>
<br>

We'll fix this by first removing the book images/descriptions every time someone hits search before loading the new images/descriptions.<br>
 
 Go to the `js` tab, and paste in the following function that will clear the book images/descriptions:
 
 ```
  PageModule.prototype.resetPage = function () {
      const col1 = document.getElementById('leftColumn');
      const col2 = document.getElementById('rightColumn');
      while (col1.firstChild) { // while there are images, remove them
        col1.removeChild(col1.firstChild);
      }
      while (col2.firstChild) { // while there are descriptions, remove them
        col2.removeChild(col2.firstChild);
      }
    };
 ```
![](/images/david-search-14.png)<br>
<br>

With this new function added, navigate to our action chain that invokes the loadImage and loadDescription functions. Add a new `module function` that calls on the resetPage function.

![](/images/david-search-15.png)<br>
<br>

![](/images/david-search-16.png)<br>
<br>

![](/images/david-search-21.png)<br>
<br>

Now go back to the `Designer` view, click the submit button, and bind this action chain to whenever someone clicks the search button. There are now three actions within this action chain. One to remove any previous search results, one to load descriptions, and the last to load images.

![](/images/david-search-17.png)<br>
<br>

Try loading the page again. It works! We have now successfully implemented the search functionality.

</details>

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
Inside the panel, at the very left, drag on a Heading component. Drag the slider bar under the General tab so that it is only H4. Call this "Username".
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
<br>
This means we are ready to set up our Service Connection. In Lab 300 we called the REST endpoint in our Javascript, but VBCS actually offers a nice feature to make REST calls without (much) coding. On the far left, hit the icon that looks like a wire with a bump in it (the third from the top) and then hit the plus sign to create a new Service Connection. Choose Define by Endpoint.<br>
![](/images/4-18.png)<br>
<br>
Now, we need our REST endpoint URL. Reopen your GrapheneDB Database, and go to the Connection tab. There you will find your HTTP REST endpoint.<br>
![](/images/4-19.png)<br>
<br>
Copy and paste that URL on VBCS, then add `/transaction/commit` to the end of it. Change Method to POST. <br>
![](/images/4-20.png)<br>
<br>
Hit next. Change Service Name to "Neo4j Get User Data". <br>
![](/images/4-22.png)<br>
<br>
Go to the Authentication tab, and choose `Basic` from the dropdown. You should have already made a database user in GrapheneDB; if not, review part 1 of this lab. Enter in the username and password for this user. <b>This is not the same as your GrapheneDB account.</b> <br>
![](/images/4-23.png)<br>
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
![](/images/4-24.png)<br>
<br>
Expand `Service Connections` and select the endpoint we just created. <br>
![](/images/4-25.png)<br>
<br>
Now we are going to append three string variables to create the request body. The first and last variables do not change; they are the main part of the request. The middle string is the searchUsername we already made. By appending all three we can change out which user we are searching for. <br>
Go back to the main page's variables. Create two Strings, getDataPt1 and getDataPt2. <br>
For getDataPt1, set this default value: `{  "statements": [   {    "statement": "MATCH (user:Person {name:  '`<br>
For getDataPt2, set this default value: `'}) return user"   }  ] }`<br>
Together with the searchUsername, it will be `{  "statements": [   {    "statement": "MATCH (user:Person {name: 'searchusername'}) return user"   }  ] }`. <br>
Go back to the action chain. Click on the REST Call action, and then click on the body paramater. <br>
![](/images/4-26.png)<br>
<br>
Drag getDataPt1, then searchUsername, then getDataPt2, onto body. <br>
![](/images/4-27.png)<br>
<br>
Great! The request should be correctly formatted. Now, to display the response, we need to do one more action. Drag a Assign Variables action onto the next step in the chain, then hit `Assign` next to `Variables`. <br>
On the left, expand callRestEndpoint1 -> body -> results -> item[0] -> data -> item[o] -> row -> item[0], until it looks like this:<br>
![](/images/4-28.png)<br>
<br>
Drag `image` on the left to `imageURL` on the right, `name` on the left to `username` on the left, and `quotes` on the left to `favoriteQuote` on the right. Then hit `Save`. <br>
![](/images/4-29.png)<br>
<br>
Test your website! Enter in AprilGold for the username, then hit search. You should see this:<br>
![](/images/4-29.png)<br>
<br>

  
</details>
