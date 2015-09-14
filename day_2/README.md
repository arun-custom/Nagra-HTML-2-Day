# HTML, CSS, JS Continued

##Introduction to DOM Manipulation
- One of the most powerful features of JS is its ability to alter the DOM.
- You can respond to events on elements, set HTML dynamically, and perform animations.

## Selecting Elements
- Like CSS, if you want to perform some action on an element you first have to select it.
- We did this in CSS through selectors such as IDs, classes, and pseudo-selectors.
- JavaScript gives us an easy way to select elements based on the same paradigm.

#### getElementById()

```
document.getElementById("my-div");
```

#### getElementsByClassName()

```
document.getElementsByClassName("my-div");
```

#### getElementsByTagName()

```
document.getElementsByTagName("my-div");
```

#### querySelector()

```
document.querySelector("#my-div");
```

#### querySelectorAll()

```
document.querySelectorAll("#my-div.my-class");
```

## Dynamically Altering Attributes
- There are many reasons why you may want to alter HTML attributes on the fly with JS.
- Changing inline CSS properties is the most common reason to alter attributes. This can be done with the `style` attribute.
- There are "getter" and "setter" methods available to work with attributes:

Getter

```
div.getAttribute("id");
```
Setter

```
div.setAttribute("style", "background-color: red;");
```

## Dealing with Classes
- In JavaScript you will often need to dynamically change HTML class attributes.
- This may be for animation work or for basic stylistic changes.
- There are a few methods you can use to accomplish this:

Add a class:

```
div.classList.add("anotherclass");
```

Remove a class:

```
div.classList.remove("foo");
```

Toggle a class:

```
div.classList.toggle("visible");
```

Check if element already contains a class:

```
div.classList.contains("foo");
```

## DOM Manipulation Exercise: Shakespeare's Plays
- Download the starter code files [here](shakespeares_plays/).
- Add a class of `special` to all of the `<li>` elements at the second level of the nested list.
- Add a class of `year` to all of the table cells in the third column of a table.
	- Hint: Take a look at how many columns are in each table.
- Make every other table row in both tables have a gray background.
- Select an anchor tag that has a link to a pdf file. Change the color to blue and increase the font size.
- Select an anchor tag that has an href attribute containing the substring "asyoulikeit" and change the font color to orange.

## Handling Events
- There are many events you may want to respond to with JS including clicks, mouseovers, focuses, etc.
- Events can be listened for and responded to using `addEventListener`.

```javascript
document.getElementById("my-div").addEventListener("click", function() {
	alert("Click worked!");
});
```

- If you need to handle an event that occurs on many elements you will need to attach event listeners to each element individually.
- This can be done by binding the event to a class. Let's take this example:

#### index.html

```html
<div class="my-div"></div>
<div class="my-div"></div>
<div class="my-div"></div>
```

#### app.js

```javascript
var myElements = document.getElementsByClassName("my-div");

for (var i = 0; i < myElements.length; i++) {
	myElements[i].addEventListener("click", function() {
		alert("Click worked!");
	});
}
```

## innerHTML
- When you need to replace the HTML inside of an element you can use the `innerHTML` property.

```javascript
document.getElementById("my-div").innerHTML = "<span>New HTML here</span>";
```

## Score Keeper Lab
- We will be creating a simple score keeper application using JavaScript.
- The HTML and CSS has already been done for you [here](score_keeper_html/).
- Here are the steps you should take:
	- Step 1: Add a link to your own custom JS file before the closing body tag.
	- Step 2: Bind click events to the +5 and -5 point buttons and change the innerHTML of the score display appropriately.
	- Step 3: Bind a click event to the set score button and set the innerHTML of the score display to the score entered in the text box.
	- **Bonus:** Create a check in your code to make sure the score will not go negative.
	- **Super Bonus:** Create a function to make the changes to the score display rather than having to write your logic over and over.

## Tic-Tac-Toe Lab
- We will be coding the game of Tic-Tac-Toe from scratch.
- There is so HTML written for you already so you will have to develop your own.
- For the basic requirements don't do any win checking.
- Make sure to account for a space that is already taken.
- **Bonus:** Check for a win and stop the game when a win is detected.

## AJAX
- AJAX is a powerful way to create server requests and get responses without having to reload the page.
- AJAX stands for Asynchronous JavaScript and XML.
- Here is how it can be accomplished:

```
function reqListener () {
	console.log(this.responseText);
}

var oReq = new XMLHttpRequest();
oReq.onload = reqListener;
oReq.open("get", "[Endpoint Here]", true);
oReq.send();
```

- XMLHttpRequest is an object that contains the methods to send AJAX requests.
- The most important method here is `.open`, which takes three parameters:
	- Type of request
	- URL endpoint
	- Asynchronous true or false
- `.send` submits the request.

## AJAX Exercise
- Let's make a request out to `http://daretodiscover.herokuapp.com/users`.
- We can evaluate how we can get data into the console about each user.

## In-Class Lab / Homework
- Make a GET request call out to `http://daretodiscover.herokuapp.com/wines`.
- Take the returned data and create a simple HTML template to show the data for each wine.

## How to Use Handlebars
- Handlebars templates are handled through `<script>` tags, which allow them to be ignored while rendering the page:

```html
<script id="my-template" type="text/x-handlebars-template">
```

- You can write any normal HTML here, but you can also write Handlebars-specific code:

```html
<script id="my-template" type="text/x-handlebars-template">
	<div class="entry">
		<h1>{{title}}</h1>
		<div class="body">
			{{body}}
		</div>
	</div>
</script>
```

- The curly code is essentially keys to a JSON object.
- If you need to, you can also loop through an array of JSON objects to produce very dynamic templates. You will do this today. Here is an example from the docs on how this can be done through helpers:

```html
<h1>Comments</h1>

<div id="comments">
	{{#each comments}}
		<h2><a href="/posts/{{id}}">{{title}}</a></h2>
		<div>{{body}}</div>
	{{/each}}
</div>
```

- This example assumes that `comments` is an array of JSON objects.
- Before a template is used however, it must be first "compiled":

```javascript
var source = document.getElementById("my-template").innerHTML;
var template = Handlebars.compile(source);
```

- The function `Handlebars.compile` returns a function that can be passed JSON data as an argument.
- This resulting function returns HTML after the JSON data is processed into it.
- You can then apply your template anywhere you need to:

```javascript
var jsonData = {
	title: "My New Post",
	body: "This is my first post!"
};

var template_html = template(jsonData);
document.getElementById("some-div").innerHTML = template_html;
```

## Book List with Handlebars
- We will be creating a simple book list system using handlebars to take care of the templating.
- The API for this exercise will be `http://daretodiscover.herokuapp.com/books`.
- The HTML is already done for you [here](book_manager_html/).