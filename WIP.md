<h2> Lab 400: Part something idk setting up on VBCS  </h2>

Let's go ahead and create an entirely new web app, as this lab does not relate to our Library website. Click the computer icon on the far left, then hit the plus sign next to Web Apps. Name it whatever you like.<br>
{img}
<br>
The first thing to do is drag and drop an Input Text component into the top left of the page. Change the label to be one column big, and change its text to say "Search Name". Move over the text field to be right next to the label, and change it to be two columns wide. To the right of that, drag on a button, and have it say "Search". <br>
{img}
<br>
In the next row, drag a Panel. By default, it fills the page horizontally, but this isn't what we want. Go to the Code view and find the `oj-panel` div. You'll see something that says "oj-sm-12 oj-md-12". These indicate the how many columns the component should take up for "small" and "medium" views of the page. For this we will be working with medium screens, so change oj-md to oj-md-5. <br>
{img}
<br>
