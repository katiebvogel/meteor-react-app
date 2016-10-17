Basic Meteor app with some practice working with a new technology for me, React!

https://www.meteor.com/tutorials/react/components

To run the application on localhost:3000 use:    $ meteor


after getting meteor started,
run
meteor npm install --save react react-dom



To allow us to create a "data container" to feed Meteor's reactive data into React's component heierarchy:  
meteor npm install --save react-addons-pure-render-mixin
meteor add react-meteor-data


See also: https://guide.meteor.com/structure.html
*notes:  

Components can receive data from there parents through attributes called "props".

In Meteor, "import" statements replace "require" syntax.  They must be used at the top-level scope, you you cannot place them within "if" satements.  


Below we see the structure with quick explanation of each file's purpose

imports/
 startup/
   client/
     index.js                 # import client startup through a single index entry point
     routes.js                # set up all routes in the app
     useraccounts-configuration.js # configure login templates
   server/
     fixtures.js              # fill the DB with example data on startup
     index.js                 # import server startup through a single index entry point

 api/
   lists/                     # a unit of domain logic
     server/
       publications.js        # all list-related publications
       publications.tests.js  # tests for the list publications
     lists.js                 # definition of the Lists collection
     lists.tests.js           # tests for the behavior of that collection
     methods.js               # methods related to lists
     methods.tests.js         # tests for those methods

 ui/
   components/                # all reusable components in the application
                              # can be split by domain if there are many
   layouts/                   # wrapper components for behaviour and visuals
   pages/                     # entry points for rendering used by the router

client/
 main.js                      # client entry point, imports all client code

server/
 main.js                      # server entry point, imports all server code


Step 6:
 -To get Meteor running on an iOS simulator (Mac Only):
 Go to your app folder and type:
meteor install-sdk iOS
meteor add-platform ios
meteor run ios
Starts your app in an ios simulator popup window.


** Having trouble with prerequisite installs.  Save mobile run for later**

Step 8:
Automatic Accounts UI!!!  
after intsalling the accounts-ui package.  See imports/ui/AccountsUIWrapper.js and imports/startup/accounts-config.js


**I added a login with facebook.  It seems to be missing a few details.  The username should show up next to the new task on the to-do list.  But moving on.

Step 9:  Security with Methods
*I ran $ meteor remove insecure
in order to remove client-side db permissions.
So we rewrote some parts of the app to use "methods", which are defined in imports/api/tasks.js.  Then we called those Meteor methods in the App.js and Task.js files. (See which code was commented out and replaced with Meteor.call)

Step 10: Filtering data with publish and subscribe
run $ meteor remove autopublish
This will hide all the tasks in the list until we give some directions to the client portion of our app.
We will use Meteor.publish and Meteor.subscribe explicity within the imports/api/tasks.js and imports/ui/App.js files

Step 10.4 Adding a button to make tasks private
method in imports/api/tasks.js
10.5 update render to show the Private buttong imports/ui/App.js
10.6 add a new prop type for the Task component in imports/ui/Task.js
10.7 Then add a button, using the new prop to decide whether or not the button should be displayed also in imports/ui/Task.js
10.8 Also define the event handler

10.9 Then install a package called classnames
$ meteor npm install --save classnames

10.10 add private ClassName to Task when needed imports/ui/Task.js

10.11 Selectively publish based on privacy status imports/api/tasks.js

10.12 Extra method security imports/api/tasks.js
this will ensure that if you didn't create the task, you can't delete it or check it off the list. UNLESS the task is set to public!!!


Step 11's:  TESTING

11.1 add a test driver for the Mocha JS test framework:
$ meteor add practicalmeteor:mocha
To run the app in test mode from now on:
$ meteor test --driver-package practicalmeteor:mocha



11.2 Add a scaffold for the method test in imports/api/tasks.tests.js
We wrote a test to make sure that a random userId can delete its own task.  If you run the app in test mode, we should get 100%!
