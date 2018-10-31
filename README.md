# VBCS Integration

<h2> Lab 100: Starting Your Web App </h2>

<h3> STEP ONE: Create Web App </h3> 

Sign in to your Cloud Account. <br>
{image here} <br>
<br>
Navigate to Cloud Dashboard, then open Visual Builder Service Console. If Visual Builder is not visible, click Customize Dashboard, then scroll to Visual Builder in the list and hit "Show".<br>
{image} <br>
<br>
At the top right of the page, hit Quick Starts. This will allow us to create the underlying infrastructure for VBCS at the same time we create the VBCS instance, rather than making them separately. Simply name the instance and then hit Create. If you don't care about configuring the database that your instance will run on, this is the way to go. <br>
Alternatively, you can hit the Customize button on the top right. This would allow you to configure the database that is created. For the purpose of this lab, we will stick to the default QuickStart configuration.
{image}<br>
<br>
Now, you need to download the generated SSH key and credentials in order to continue. These allow you to access your instance.<br>
{image}<br>
<br>
Your instance will take some time to provision. When it's ready, you can open the Visual Builder Home page.<br>
{image}<br>
<br>
Now we need to create a Visual Application. From the home page, hit New in the top right. <br>
{image}<br>
<br>
Name it whatever you like. Description is optional. <br>
{image}<br>
<br>
Your new Application should open automatically. On the left, hit the computer icon for Web Apps, then create new. Name it whatever you like. <br>
[image]<br>
<br>
Expand flows, then main, then click on main-start. <br>
This will show a blank page in the center, with a components bar to the left, and a customization bar on the right.<br>
[image]<br>
<br></p>
<h3> STEP TWO: Customize Web App</h3>
<p>
Click on the Design view tab in the top right. Drag on an image component into the very top left corner of the page. <br>
Click on it, then look on the right side go to the Data tab. Put in https://png.icons8.com/color/1600/reflector-bulb.png for the source url. <br>
{image showing data tab}<br>
<br>
However, the image is huge, which we do not want. Go to the General tab and set width to 150. Much better. <br>
{image}<br>
<br>
Next drag on a Heading component one column to the right of the logo. In the General tab, inside the Text field put whatever you want your website to be called.<br>
In the row below, drag a tab bar. It defaults to three tabs, but we only need two for now. Hover over tab 3 in the General tab, then hit the trash can icon.<br>
Drag and drop another Heading component, and fill in "Welcome to the Home page" for text.<br>
It should now look something like this.<br>
[image showing all four components]<br>
<br>
Let's say we want to change the color of this text. Click on the Heading and go to the All tab, then expand General Attributes and scroll down to the Style field. Enter in "color: #67aee5;" (without the quotes). The color changes to a light blue. This is an easy way to customize the CSS for a specific component. <br>
[image]<br>
<br>
However, we can also edit the HTML and CSS more directly. Near the top right, hit the Code tab for the page. <br>
[image]<br>
<br>
To customize the tab bar, we will first define some style. <br>
[Show code]<br>
We will add this to our tabs, with dull being for the tab we are currently on, and bright being for the tab we are not on.<br> [Show code]<br>
Back on the design tab, we can view the changes to the tab bar. This gives you much greater flexibility.<br>
[image]<br>
<br></p>
<h3> STEP THREE: Add Navigation </h3>
<p>
Now, for this tab bar to actually navigate the website, we need a second page to navigate <i>to</i>. Go to the Web App heirarchy on the left and hit the plus sign next to main in order to create a new page. Name this something like second-page. <br>
[image]<br>
<br>
Paste in the code from the first page, switching which tab is dull and which tab is bright. <br>
[image]<br>
<br>
On the Design view, change Welcome to the Home Page to say Welcome to the Second Page. The page should look like this.<br>
[image]<br>
<br>
Next, we want to create some events and action chains. These will allow us to navigate to the second page and back again when a tab is clicked.<br>
Go to the main flow’s page, and hit actions. Creating an action chain at the flow level allows us to reuse these components on each page.<br>
Create new action chain and call it something like navigateHome. <br>
[image]<br>
<br>
Drag and drop a Navigate component to the plus sign, then click Select Target.<br>
[image]<br>
<br>
Choose Peer Page, and then main-start.<br>
[image]<br>
<br>
Repeat this process for a navigateSecondPage action chain, this time selecting second-page as target.<br>
Now, go back to main-start and tab to Events. Near the top-right hit Event Listener, then create a new Custom Event. Call this something like clickHomeTab. <br>
[image]<br>
<br>
On the next page, select navigateHome for the action chain.<br>
[image]<br>
<br>
Repeat this process for clickSecondTab and navigateSecondPage.<br>
Then create these same events in the second-page events.<br>
<br>
Last but not least, we want to connect these event listeners to our tabs so that the action chains will be run.<br>
Go to Code view and insert on-click="[[$listeners.eventName]]" where eventName is the name of your event for each tab (i.e., clickHomeTab and clickSecondTab). <br>
[show pic where to insert code]<br>
<br>
Note, many components have an Events tab that allows you to create events containing an action chain all in one click, but because we want different parts of the tab bar to take us to different pages, we have to do it manually.<br>
The Events tab is very useful for things such as buttons, where you can quickly create an action for when the button is clicked.<br>
<br>
Finally, put in the listners for the second page, and you should be good to go! You now have a functional website.<br>
Click on the play button in the top right to test your website, seeing that you can navigate between the two pages.<br>
</p>
