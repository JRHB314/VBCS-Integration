# VBCS_Integration
<h1> Lab 100: Creating Your Web App </h1>

<p>
Sign in to Cloud Account, open VBCS Service Console.
In the top right, hit New and then name application.
On the left, hit the computer icon for Web Apps, then create new. 
Expand flows, then main, then click on main-start. This will show a blank page in the center, with a components bar to the left, and a customization bar on the right.
Drag on an image component into the very top left corner of the page. 
Click on it, then on the right side go to the Data tab. Put in [url] for the source url. 
Next drag on a Heading component one column to the right of the logo. In the General tab, put in Text [website name].
In the row below, drag a tab bar. It defaults to two tabs, which is fine for now. We will be adding more later.
Drag and drop a Heading component, and fill in Welcome to the Home Page for text.
Notice how it presses right up against the tab bar. It looks nicer to have some space between the two. 
Click on the bar and go to the All tab, then expand General Attributes if it is collapsed. 
Scroll down to the style box, and put in “margin-bottom: 50px;” (without the quotes). This is an easy way to customize the css for a specific component. 
However, we can also edit the html and css more directly. Near the top right, hit the Code tab for the page. 
To customize the tab bar, we will first define some style. [Show code]
We will add this to our tabs, with dull being for the tab we are currently on, and bright being for the tab we are not on. [Show code]
First off, a second page must exist in order to navigate to it. Go to the Web App heirarchy on the left and hit the plus sign next to main in order to create a new page. Name this something like second-page.
Paste in the code from the first page, switching which tab is dull and which tab is bright. On the Design view, change Welcome to the Home Page to say Welcome to the Second Page.
Next, we want to create some events and action chains. These will allow us to navigate to the second page and back again when a tab is clicked.
Go to the main flow’s page, and hit actions. Creating an action chain at the flow level allows us to reuse these components on each page.
Create new action chain and call it something like navigateHome. 
Drag and drop a Navigate component to the plus sign, then click Select Target. Choose Peer Page, and then main-start.
Repeat this process for a navigateSecondPage action chain, this time selecting second-page as target.
Now, go back to main-start and tab to Events. Near the top-right hit Event Listener, then create a new Custom Event. Call this something like clickHomeTab. 
On the next page, select navigateHome for the action chain.
Repeat this process for clickSecondTab and navigateSecondPage.
Then create these same events in the second-page events.
Last but not least, we want to connect these event to our tabs so that the action chains will be run.
Go to code [show pic where] and insert on-click="[[$listeners.eventName]]" where eventName is the name of your event for each tab (ie, clickHomeTab and clickSecondTab). 
Repeat this for the second page, and you should be good to go! You now have a functional website.
</p>
