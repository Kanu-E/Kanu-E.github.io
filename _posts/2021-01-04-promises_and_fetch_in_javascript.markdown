---
layout: post
title:      "PROMISES AND FETCH IN JAVASCRIPT"
date:       2021-01-04 17:37:33 +0000
permalink:  promises_and_fetch_in_javascript
---

When a user tries to access a webpage she will do so by sending a HTTP request, the browser tends to wait till all the data has to be accessed has fully loaded  in the meantime the users browser will display a blank page . When there is large data to be processed, this may take a while and result in an unsatisfactorily user experience.

The fetch function is a function that allows us to send network requests with the value as some kind of data and said data can be loaded when needed without the need to reload a page.

This blog will give a slight insight into how the fetch function can be used to display data.

The fetch function can both receive Information (**get request**) and send information (**post Request**). to carry out a simple fetch request the first thig the program will do is call the fetch function with a single argument (the path to the resource).

```
fetch('a string indicating the file location')
```

This comes back with a response object which is a [promise](http://www.w3schools.com/js/js_promise.asp) and if it is successful, we get a stream of data that we will need to handle and since it is a promise, this could be done using a `.then()`  method which takes in the stream of data that we got from the fetch method above and put the response as and argument and ;

```
fetch('a string indicating the file location')
.then((response =>{ response.action()
}) 

```

This will give another promise that if resolved, would have completed reading the stream of data and turned it into the format you wanted thereafter you can use the then method to to display as you wish.

```
fetch('a string indicating the file location')
.then((response =>{ response.action()
}) ;
.then(formattedResponse => {manipulate the DOM to display data);

```

Let's take a look at a possible example. We are going to fetch an image of Rick from Rick and Morty using the restful [API](https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/) for the series and display it in a HTML file

```
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Workings</title>
  </head>

  <body>
    <img src"" id ="rick">
   
    <script>
 fetch('https://rickandmortyapi.com/api/character/1')
 .then(resp => resp.json())
 .then(json => (document.getElementById("rick").src = json.image));
		
		</script>

</html>

```
And there you have we used the fetch method and passed ('https://rickandmortyapi.com/api/character/1') as an argument  to get a stream of data,  we *then* handled it by transforming it into a [json](https://www.w3schools.com/js/js_json_intro.asp) and then displayed the image in the DOM.


