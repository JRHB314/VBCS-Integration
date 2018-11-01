<h2> Lab 400: Connecting VBCS to MongoDB </h2>

MongoDB is a very popular database, and it offers a bit more customization on its backend than Firebase does. This allows us to perform filtered queries more easily. 

<details><summary>1. Set up MongoDB Database</summary>

<h2>Set up MongoDB</h2>

Add data of books to DB.<br>
Compare and contrast to Firebase.<br>
Connect it to VBCS.<br>
Show list of books on Web App.<br>

</details>




<details>
  <summary>3. Creating a Search Page </summary>
  
  <h3> Creating the Website's Search Functionality </h3>
  
  Let's review what we've done until this point. So far, we've built our web application, created a Firebase database and populated it with information, and wrote custom Javascript to extract data from our database URL. We invoked those functions and had them run at page load time, and we were able to display book images and descriptions on our catalog page. Great! But what if we want to display books based on a user search? That takes a bit of extra work. We'll need to first capture the user's input, and then parse our JSON object accordingly.<br>
  
  First create a third page for this website's search functionality. We'll call it "search". Duplicate `main-start` and rename the copy `search`.<br> 
Change "Welcome to the Home page." to say "Search". Drag and drop a `user input` box for the user to type in their search term, followed by a `button` for running that search. Click on the `Input Text` label and change it to say "Genre:".Let's also drag over a button to the right of the input text. Change the text of the button to "search".<br> 
 
 ![](/images/3-ds3.png)<br>
<br>

Note, however, that we only have three tabs; we need to make one more tab for the new page. Follow the instructions in the previous step for creating a new tab, but this time for searchpage.<br>
Briefly,<br>
-Copy and paste code for a new tab in each page.<br>
-Change the tab name to "Search" and the onclick listener to clickSearchTab.<br>
-Create an action chain navigateSearchPage at the flow level.<br>
-Create an event listener on each page called clickSearchTab.<br>
 
 We have a nice simple layout. We need to now save the user's input into a variable. On the left side under the `variable` function, create a new variable. Call it `genre`.<br>
 
 ![](/images/david-search-5.png)<br>
<br>
 
 Go back to the search page and click on the text input box. Under `Data`, enter `{{ $page.variables.genre }}`. This saves the value that the user types into our genre variable.
 
 ![](/images/david-search-6.png)<br>
<br>
 
 Next, let's copy over the Javascript code. Under the `js` tab of our catalogue page, copy and paste the two slightly modified functions below onto our search page. 
 
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
 
 ![](/images/david-search-12.png)<br>
<br>
 
Try hitting the search button again. Uh oh, looks like the page is getting populated with the same books every time someone hits search. 

![](/images/david-search-13.png)<br>
<br>

We'll fix this by first removing the book images/descriptions before someone hits search.<br>
 
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

![](/images/david-search-19.png)<br>
<br>

Now go back to the `Designer` view, click the submit button, and bind this action chain to whenever someone clicks the search button. There should be 2 events binded to the search button: one that loads the images/descriptions, and now another one that clears the page.

![](/images/david-search-17.png)<br>
<br>

Try loading the page again. It works! We have now successfully implemented the search functionality.

![](/images/david-search-20.png)<br>
<br>

</details>
