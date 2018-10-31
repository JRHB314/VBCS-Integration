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
  
  In the row below, drag over a tab bar. The tab bar defaults to three tabs, but we only need two for now. Hover over `Tab 3`   in the General tab, then hit the trash can icon.<br>
  
  ![](/images/17.png)<br>
  
  Drag and drop another Heading component, and fill in "Welcome to the Home page" for the text.<br>
  
  Let's say that we want to customize the color of the text that we just entered. Click on the Heading, go to the `All` 
  tab, then expand `General Attributes` and scroll down to the `Style` field. Enter in `color: #67aee5;`. The color 
  changes to a light blue. This is an easy way to customize the CSS for a specific component. <br>
  
  ![](/images/18.png)<br>
  <br>
  
  In addition, we can also edit the HTML and CSS code directly. Near the top right, hit the `Code` view for the page. <br>
  
  ![](/images/19.png)<br><br>
  
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

  ![](/images/20.png)<br><br>
  
  Back on the design tab, we can view changes we made to the tab bar. As demonstrated, you can code HTML and CSS for your web   app the way you would for any website while also viewing it in the Design tab, giving you much greater flexibility.<br>
  
  ![](/images/21.png)<br>
  <br>
  
 </details>
  
<details>
  <summary>3. Add Navigation</summary>

  <h3>Add Navigation </h3>

  In order for this tab bar to actually navigate the website, we need a second page to navigate <i>to</i>. Go to the Web App 
  heirarchy on the left and hit the plus sign next to `main` in order to create a new page. Give this new page a name. For 
  this lab, we'll name the page "second-page". <br>
  
  ![](/images/33.png)<br>
  <br>
  
  Because we want the navbar to remain on this second page as well, copy the code from the first page and paste it into the 
  code for second-page. Or alternatively, right click on main-start and hit `Duplicate`. <br>
  
  You'll see part of the code is underlined in red. Click within it, and then add `Add Missing Dependencies`. When a component 
  is dragged onto the page, it automatically adds in the dependencies. However, if you copy and paste code directly, you'll have to add the missing dependencies yourself.<br>
  
  ![](/images/22.png)<br>
  <br><br>
  
  Switch which tab is dull and which tab is bright. Dull tabs represent the current page we're on. <br><br>
  ![](/images/23.png)<br>
  <br>
  
  On the Design view, change "Welcome to the Home Page" to say "Welcome to the Second Page". It should look like this.<br>
  ![](/images/24.png)<br>
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
  
  Repeat this process for creating clickSecondTab and having it trigger navigateSecondPage.<br>
  Then, create these same events for second-page.<br>
  
  ![](/images/32.png)<br>
  <br>
  
  Last but not least, we want to connect these event listeners to be activated whenever our tabs are clicked. Go to Code view,   and add the onclick listener after the li id for both tabs. Enter
  
  ```
  <li id ="oj-tab-bar-XXXXXXXXX-X-tab-X" on-click="[[$listeners.eventName]]"
  ``` 
  
  where eventName is the name of your event for each tab (i.e., clickHomeTab and clickSecondTab). <br>
  
  <br>
  ![](/images/34.png)<br>
  <br>
  
  Note that many components have an Events tab that allows you to create an event and action chain all in one click, but    
  because we want different parts of the tab bar to take us to different pages, we have to set them up manually.<br>
  The Events tab is very useful for things such as buttons, where you can quickly create an action for when the button is 
  clicked.<br><br>
  
  Finally, add the onclick listeners for the second page, and you should be good to go! You now have a functional website.<br>
  <br>
  
  Click on the play button in the top right to test your website, seeing that you can navigate between the two pages.<br>
  
  ![](/images/7.png)<br>
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
  
  <h3> Add HTML/CSS </h3>
  
  Now that our database has been set up, we'll need to connect it to VBCS. We'll be using this database information to populate one of our pages with images and descriptions of books, so the first thing we need to do is to come up with a layout of how we want our page to look. For this lab, we'll format the page with a left-side column to display book images and a right-side column to display the book information.<br>
  
  Let's create this layout by adding the HTML structure to our existing second page. Navigate to the `Code` view of the page, and copy and paste this HTML code and add it at the very end:<br>

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
  ![](/images/david-1.png)<br>
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
So in the end it will look like:
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

We want this function to be called on page load. Go to Events for the {pageName} page.<br>
Click Create Event Listener, then under Lifecycle Events, select vbEnter. This will be an event that runs when the page loads.<br>
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
Add another action change under vbEnter, this one called runLoadImages. Set it up the same as runLoadDescriptions, with this one calling the loadImages module.<br>
<br>
Test the page one more time, and we should see the book covers to the left of the book descriptions. <br>
![](/images/3-21.png)<br>
<br>
Great job!
  
</details>


  
