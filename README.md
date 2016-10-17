Basic Meteor app with some practice working with a new technology for me, React!

https://www.meteor.com/tutorials/react/components


after getting meteor started,
run
meteor npm install --save react react-dom



To allow us to create a "data container" to feed Meteor's reactive data into React's component heierarchy:  
meteor npm install --save react-addons-pure-render-mixin
meteor add react-meteor-data


See also: https://guide.meteor.com/structure.html
*notes:  

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
