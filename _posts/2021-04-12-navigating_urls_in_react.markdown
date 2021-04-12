---
layout: post
title:      "Navigating URLS in React"
date:       2021-04-12 14:32:38 -0400
permalink:  navigating_urls_in_react
---

React is an amazing tool for the creation of a single page application so we only need to make one get request to the server, but in many cases, user experience might require an application to have more than a single page. Normally switching URLs will require the server to be called up each time. This is were react’s client-side routing comes in. With client-side routing, you are able to use JSX components as separate URLs without the need to reload the page from the server side.
This result in a better user experience as switching between pages are a lot faster.
So how do we add client-side routing to our React app? React router helps with ensuring the UI matches URL

## Let's see react router at work
The package that will be needed to be installed in order to access react router is the react-router-dom. This will give us access to some objects that we can use in our JSX.
Let's assume we have a simple react app that we will like to add some components with client-side routing to, it may look like this.

```
import React from "react";
import ReactDOM from 'react-dom';

const App = () => {
 return (
   <div className="App">
   	<h1>React Router </h1>
   </div>
 );
};
export default App;
 - -
 
ReactDOM.render(<App />, document.getElementById("root"));
```

This code above has a single App component that is being rendered in the DOM.
Let's modify the app to have the following pages;
* Home 
* About
* Contacts
To start using routes in the app, we will have to install the react-router-dom package and import BrowserRouter and Route from react-router-dom. It is convention to import BrowserRouter as Router so this is what we will use. The BrowserRouter (which we will give the Router alias) is the base for the entire application. We will also wrap the App Component with the Router

```
import React from "react";
import ReactDOM from 'react-dom';
import { BrowserRouter as Router } from 'react-router-dom';
  const App = () => {
   return (
     <div className="App">
          <h1>React Router App </h1>
     </div>
   );
  };
  export default App;
 
ReactDOM.render( 
   <Router>
      <App/>
   </Router>, 
document.getElementById("root"));

```

After the Router is set up, we will want to set up the components for the application we will like to and figure out a way we can navigate to those components in our browser. In order to do this, we will need to import the route component from react-router-dom and declare the Route component on the App component

```
import React from "react";
import { BrowserRouter as Router, Route } from 'react-router-dom';
import ReactDOM from 'react-dom';

const App = () => {
  return (
    <div >
        <Route path="/" component={Home} />
       	<Route path="/about" component={About} />
        <Route path="/contacts" component={Contacts} />
          
     </div>
  );
};

export default App;

  
ReactDOM.render(   
      <Router>
           <App/>
      </Router>, 
document.getElementById("root"));

const Home = () => {
  return (
    <div>
      <h1>This is Our Home Page !</h1>
    </div>
  );
};
 
const About = () => {
  return (
    <div>
      <h1>This is My about Page!</h1>
    </div>
  );
};

const Contacts = () => {
  return (
    <div>
      <h1>This is My Contact Page!</h1>
    </div>
  );
};
```

If you open up the browser, the above code will display the Home component when the URL is /and will display the About and Contacts component for /about and /contacts respectively. It will however display the contents of the Home components when you navigate to other URLs as shown below:

![](https://ibb.co/vZRd4J6)

Having this might be useful in situations were we have a heading that will will like to show on every page or where you want details of another component to show while rendering another's URL but it might not be suitable in some. In those instances, we can fix it so that the contents of the Home aren't displayed when we navigate to a URL nested in the home URL we can change our Route component for Home to exact path instead of just path

```
import React from "react";
import { BrowserRouter as Router, Route } from 'react-router-dom';
import ReactDOM from 'react-dom';
 
const App = () => {
  return (
    <div >
        <Route exact path="/" component={Home} />
       	<Route exact path="/about" component={About} />
        <Route exact path="/contacts" component={Contacts} />
          
     </div>
  );
};
 
export default App;
 
---
```

With the exact attribute passed, we are explicitly stating that we only want to see the specific component rendered when we go to the route that matches said component.

