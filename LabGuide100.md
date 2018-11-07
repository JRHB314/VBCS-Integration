
![](images/100/Picture100-lab.png)  
Updated: November 6, 2018

## Introduction

This is the first of several labs that will show how to integrate different kinds of databases with VBCS. It will lead you through customizing your Web App, creating different kinds of databases, and finally, connecting them with your web page.

This lab will start with creating your first Web App in VBCS. 

**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives
- Create VBCS Instance 
- Create Web App
    - Add some design elements
    - Add navigation

## Required Artifacts
- The following lab requires an Oracle Public Cloud account; you can sign up for a trial account [here](https://cloud.oracle.com/tryit). 

# Lab 100

## VBCS: Creating Your First Web App

### **STEP 1**: Getting Started

<details>
  <summary>Sign in to your Cloud Account</summary>

  Go to the [Cloud sign in page](https://cloud.oracle.com/en_US/sign-in).

  Sign in to your Cloud Account. <br>
  ![](/images/lab100/100-1.png) <br>
  ![](/images/lab100/100-2.png) <br>
  <br>

  Navigate to Cloud Dashboard, then open the Visual Builder Service Console. If Visual Builder is not visible, click `Customize Dashboard`, then scroll to Visual Builder in the list and hit `Show`.<br>

  ![](/images/lab100/100-3.png) <br> <br>
  
</details>

<details>
  <summary>Create Visual Builder Instance</summary>

  At the top right of the page, hit "Quick Starts". This will allow us to create the underlying infrastructure for VBCS at the same time that we create the VBCS instance rather than making them separately. Simply name the instance and then hit `Create`. If you don't care about configuring the database that your instance will run on, this is the way to go. 

  Alternatively, you can hit the `Customize` button on the top right. This would allow you to configure the database that is created. For the purpose of this lab, we'll stick to the default QuickStart configuration.

  ![](/images/lab100/100-5.png)<br><br>

  Next, download the generated SSH key and credentials in order to continue, which will allow you to access your instance.

  <br>![](/images/lab100/100-12.png)<br>
  <br>

  Your instance will take some time to provision. When it's ready, open the Visual Builder Home page.

  <br>![](/images/lab100/100-8.png)<br>
  <br>

  Now, we need to create a Visual Application. A single Visual Application can hold many mobile and web apps. From the home page, hit `New` in the top right. 

  <br>![](/images/lab100/100-9.png)<br>
  <br>

  Name the application whatever you like; the Description is optional. 

  <br>![](/images/lab100/100-10.png)<br>
  <br>

  Your new Application should open automatically. 
</details>

### **STEP 2**: Creating a Web App

<details>
  <summary>Customize Web App</summary>

  On the left, hit the computer icon for `Web Apps`, then the plus sign to create a new Web App. Name it, then hit `Create`. 

  <br>![](/images/lab100/100-11.png)<br>
  <br>

  A blank page will open in the center, with a Components Bar to the left and a Customization Bar on the right.<br>
  
  ![](/images/lab100/100-14.png)<br>
  <br>
  
  Click on the `Design` view tab in the top right. Drag on an image component into the very top left corner of the page.<br>
  Click on it, then look on the right side go to the Data tab. Put in `https://png.icons8.com/color/1600/reflector-bulb.png` 
  for the source url. This image will act as our website's logo.<br> 
  
  As it is, the image size is bigger than what we'd expect for our logo, so let's resize it. 
  
  <br>![](/images/lab100/100-15.png)<br><br>
  
  Go to the `General` tab and set the `width` property to 150. Now that the image is resized, it looks much more fitting to be   our website's logo.<br>
  
  ![](/images/lab100/100-16.png)<br>
  <br>
  
  Next, drag on a `Heading` component one column to the right of the logo. Under the `General` tab inside the `Text` field,   
  enter whatever name you'd like your website to be called.<br>
  
  In the row below, drag over a tab bar. The tab bar defaults to three tabs, but we only need two for now. Hover over `Tab 3`   in the General tab, then hit the trash can icon. Rename the tabs `Home` and `Second Page`.<br>
  
  ![](/images/lab100/100-17.png)<br>
  ![](/images/lab100/100-1-17.5.png)<br>
  
  Drag and drop another Heading component, and fill in "Welcome to the Home page" for the text. While we're at it, let's customize the color of the text that we just entered. Click on the Heading, go to the `All` 
  tab, then expand `General Attributes` and scroll down to the `Style` field. Enter in `color: #67aee5;`. 
  
  ![](/images/lab100/100-18.png)<br>
  
  The heading color changes to a light blue, as shown below. This is an easy way to customize the CSS for a specific component. <br>
  
  ![](/images/lab100/100-1-18.png)<br>
  <br>
  
  In addition, we can also edit the HTML and CSS code directly. Near the top right, hit the `Code` view for the page. <br>
  
  ![](/images/lab100/100-1-19.png)<br><br>
  
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

  ![](/images/lab100/100-1-20.png)<br><br>
  
  Back on the design tab, we can view changes we made to the tab bar. As demonstrated, you can code HTML and CSS for your web   app the way you would for any website, while also having the option to change it in the Design view, giving you much greater flexibility.<br>
  
  ![](/images/lab100/100-1-21.png)<br>
  <br>
  
 </details>
  
<details>
  <summary>Add Navigation</summary>

  <br>In order for this tab bar to actually navigate the website, we need a second page to navigate <i>to</i>. We want to carry over the components from the first page to this home page (logo, title, navbar) so we'll go ahead and copy it. Go to the Web App heirarchy on the left, right click on main-start and hit `Duplicate`. Then rename the page `second-page`. On the `Code` view, paste the code we copied.<br>
  
  ![](/images/lab100/100-1-33.png)<br>
  <br>
  
  Switch which tab is dull and which tab is bright in the code section of this second page. Dull tabs represent the current page we're on. <br><br>
  ![](/images/lab100/100-1-23.png)<br>
  <br>
  
  On the Design view, change "Welcome to the Home Page" to say "Welcome to the Second Page". It should look like this.<br>
  ![](/images/lab100/100-7.png)<br>
  <br>
  
  Next, let's create some <i>events</i> and <i>action chains</i>. These will allow us to navigate to the second page and back 
  again whenever a specific tab is clicked, rather than the text itself.<br>
  
  Click on flow `main`, and hit the flag icon near the left to open up `Actions`. Creating an action chain at the flow level 
  allows us to reuse these components on each page.<br>
  
  ![](/images/lab100/100-25.png)<br>
  <br>
  
  Hit `+ Action Chain` to create a new action chain and call it something like `navigateHome`. <br>
  Drag and drop a Navigate component to the plus sign, then click `Select Target`.<br>
  
  ![](/images/lab100/100-26.png)<br>
  <br>
 
  Choose `Peer Page`, and then `main-start`.<br>
  
  ![](/images/lab100/100-27.png)<br>
  ![](/images/lab100/100-28.png)<br>
  <br>
  
  Create this process for a navigateSecondPage action chain, this time selecting second-page as target.<br>
  
  Events need to be created at the page level, because the event that triggers your action happens on a particular page. Go     back to main-start and click on the bell icon near the left to go to Events. Hit `+ Event Listener`.
  
  ![](/images/lab100/100-29.png)<br>
  <br>
  
  Scroll down to "Other Events" and hit the plus sign. Call this something like `clickHomeTab`. When done, hit `Select`.<br>
  
  ![](/images/lab100/100-30.png)<br>
  <br>
  
  On the next page, select `navigateHome` for the action chain, then hit `Select`.<br>
  ![](/images/lab100/100-31.png)<br>
  <br>
  
  Repeat this process for creating clickSecondTab and having it trigger navigateSecondPage.<br>
  Then, create these same events for second-page.<br>
  
  ![](/images/lab100/100-32.png)<br>
  <br>
  
  Last but not least, we want to connect these event listeners to be activated whenever our tabs are clicked. Go to Code view,   and add the onclick listener after the lid for both tabs. Enter
  
  ```
  <li id ="oj-tab-bar-XXXXXXXXX-X-tab-X" on-click="[[$listeners.eventName]]"
  ``` 
  
  where eventName is the name of your event for each tab (i.e., clickHomeTab and clickSecondTab). <br>
  
  ![](/images/lab100/100-1-34.png)<br>
  <br>
  
  Note that many components have an Events tab that allows you to create an event and action chain all in one click, but    
  because we want different parts of the tab bar to take us to different pages, we have to set them up manually.<br>
  The Events tab is very useful for things such as buttons, where you can quickly create an action for when the button is 
  clicked.<br><br>
  
  Finally, add the onclick listeners for the second page, and you should be good to go! You now have a functional website.<br>
  <br>
  
  Click on the play button in the top right to test your website, seeing that you can navigate between the two pages.<br>
  
  ![](/images/lab100/100-1-7.png)<br>
  <br>
</details>
