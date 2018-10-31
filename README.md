# VBCS Integration

<h2> Lab 100: Starting Your Web App </h2>

<h3> STEP ONE: Create Web App </h3> 

Sign in to your Cloud Account. <br>
![](/images/1.png) <br>
![](/images/2.png) <br>
<br>
Navigate to Cloud Dashboard, then open Visual Builder Service Console. If Visual Builder is not visible, click Customize Dashboard, then scroll to Visual Builder in the list and hit "Show".<br>
![](/images/3.png) <br> 
<br>
At the top right of the page, hit Quick Starts. This will allow us to create the underlying infrastructure for VBCS at the same time we create the VBCS instance, rather than making them separately. Simply name the instance and then hit Create. If you don't care about configuring the database that your instance will run on, this is the way to go. <br>
Alternatively, you can hit the Customize button on the top right. This would allow you to configure the database that is created. For the purpose of this lab, we will stick to the default QuickStart configuration.
![](/images/5.png)<br>
<br>
Now, you need to download the generated SSH key and credentials in order to continue. These allow you to access your instance.<br>
![](/images/12.png)<br>
<br>
Your instance will take some time to provision. When it's ready, you can open the Visual Builder Home page.<br>
![](/images/8.png)<br>
<br>
Now we need to create a Visual Application. From the home page, hit New in the top right. <br>
![](/images/9.png)<br>
<br>
Name it whatever you like. Description is optional. <br>
![](/images/10.png)<br>
<br>
Your new Application should open automatically. On the left, hit the computer icon for Web Apps, then the plus sign to create a new Web App. Name it, then hit Create. <br>
![](/images/11.png)<br>
<br>
A blank page will open in the center, with a components bar to the left, and a customization bar on the right.<br>
![](/images/14.png)<br>
<br>
<h3> STEP TWO: Customize Web App </h3>

Click on the Design view tab in the top right. Drag on an image component into the very top left corner of the page. <br>
Click on it, then look on the right side go to the Data tab. Put in https://png.icons8.com/color/1600/reflector-bulb.png for the source url. However, the image is huge, which we do not want. <br>
![](/images/15.png)<br>
<br>
Go to the General tab and set width to 150. Much better. <br>
![](/images/16.png)<br>
<br>
Next drag on a Heading component one column to the right of the logo. In the General tab, inside the Text field put whatever you want your website to be called.<br>
In the row below, drag a tab bar. It defaults to three tabs, but we only need two for now. Hover over Tab 3 in the General tab, then hit the trash can icon.<br>
![](/images/17.png)<br>
<br>
Drag and drop another Heading component, and fill in "Welcome to the Home page" for text.<br>
Let's say we want to change the color of this text. Click on the Heading and go to the All tab, then expand General Attributes and scroll down to the Style field. Enter in "color: #67aee5;" (without the quotes). The color changes to a light blue. This is an easy way to customize the CSS for a specific component. <br>
![](/images/18.png)<br>
<br>
However, we can also edit the HTML and CSS more directly. Near the top right, hit the Code view for the page. <br>
![](/images/19.png)<br>
<br>
To customize the tab bar, we will first define some style. Simply paste this at the top of the Code page.<br>
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
We will add this style as div classes to our tabs, with dull being for the tab we are currently on, and bright being for tabs we are not on.<br> 

![](/images/20.png)<br>
<br>
Back on the design tab, we can view the changes to the tab bar. In this way, you can code HTML and CSS for your web app the way you would for any website, giving you much greater flexibility.<br>
![](/images/21.png)<br>
<br>
<h3> STEP THREE: Add Navigation </h3>

Now, for this tab bar to actually navigate the website, we need a second page to navigate <i>to</i>. Go to the Web App heirarchy on the left and hit the plus sign next to main in order to create a new page. Name this something like second-page. <br>
![](/images/33.png)<br>
<br>
Copy the code from the first page and paste it into the code for second-page. Alternatively, we can right click on main-start and hit Duplicate. You'll see part of the code is underlined in red. Click within it, and then say Add Missing Dependencies. When a component is dragged onto the page, it automatically adds in the dependencies, but if you copy and paste code, you have to do this.<br>
![](/images/22.png)<br>
<br>
Switch which tab is dull and which tab is bright. <br>
![](/images/23.png)<br>
<br>
On the Design view, change Welcome to the Home Page to say Welcome to the Second Page. The page should look like this.<br>
![](/images/24.png)<br>
<br>
Next, we want to create some events and action chains. These will allow us to navigate to the second page and back again when a tab is clicked.<br>
Click on flow "main", and hit the flag icon near the left to open up Actions. Creating an action chain at the flow level allows us to reuse these components on each page.<br>
![](/images/25.png)<br>
<br>
Hit "+ Action Chain" to create a new action chain and call it something like navigateHome. <br>
Drag and drop a Navigate component to the plus sign, then click Select Target.<br>
![](/images/26.png)<br>
<br>
Choose Peer Page, and then main-start.<br>
![](/images/27.png)<br>
![](/images/28.png)<br>
<br>
Repeat this process for a navigateSecondPage action chain, this time selecting second-page as target.<br>
<br>
Events need to be created at the page level, because the event that triggers your action happens on a particular page. Go back to main-start and click on the bell icon near the left to go to Events. Hit "+ Event Listener".
![](/images/29.png)<br>
<br>
Scroll down to "Other Events" and hit the plus sign. Call this something like clickHomeTab. When done, hit Select.<br>
![](/images/30.png)<br>
<br>
On the next page, select navigateHome for the action chain, then hit Select.<br>
![](/images/31.png)<br>
<br>
Repeat this process for creating clickSecondTab and having it trigger navigateSecondPage.<br>
Then create these same events for second-page.<br>
![](/images/32.png)<br>
<br>
Last but not least, we want to connect these event listeners to be activated when our tabs are clicked. Go to Code view and add the onclick listener after the li id for both tabs.
```
<li id ="oj-tab-bar-XXXXXXXXX-X-tab-X" on-click="[[$listeners.eventName]]"
``` 
Where eventName is the name of your event for each tab (i.e., clickHomeTab and clickSecondTab). <br>
![](/images/34.png)<br>
<br>
Note, many components have an Events tab that allows you to create an event and action chain all in one click, but because we want different parts of the tab bar to take us to different pages, we have to do this manually.<br>
The Events tab is very useful for things such as buttons, where you can quickly create an action for when the button is clicked.<br>
<br>
Finally, add the onclick listeners for the second page, and you should be good to go! You now have a functional website.<br>
Click on the play button in the top right to test your website, seeing that you can navigate between the two pages.<br>
![](/images/7.png)<br>
<br>
