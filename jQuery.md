# jQuery

A JavaScript library designed to shorten the code.

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>

Add the above script tag from the google CDN (Content Delivery Network) immediately **above** our local script tag.

Or we can add the library locally by downloading it.

* [jquery-3.7.1](./jquery-3.7.1.js)
* [jquery-3.7.1.min](./jquery-3.7.1.min.js)

[Download Link](https://jquery.com/download/)

```javascript 
document.querySelector('h1')
// TO
$('h1')
```

If we want to include the scripts at the head, we need the `ready` method, so that the JavaScript is only executed after loading the page.

```javascript
$(document).ready(function() {
    // ...code...
})
```

The jQuery library (as with most libraries, like bootstrap) come with  JavaScript file `jquery.js` and another minified version of the JavaScript file `jquery.min.js`.

### Common Methods

```javascript 
// Selecting all buttons is the same as selecting one button
$('button');
```
```javascript 
// Change the styles
console.log($('h1').css('color')); // Prints the colour of h1
$('h1').css('color', 'red'); // Change the color to red
```
```javascript 
// Add / Remove a class to an element
$('h1').addClass('display-1');
$('h1').removeClass('display-1');

// Add multiple classes
$('h1').addClass('class1 class2 class3');

// Check whether an element has a class
$('h1').hasClass('display-1'); // Returns true or false
```
```javascript 
// Change the text inside an element (innerText)
$('h1').text("new text");
// Change the html inside an element (innerHTML)
$('h1').html("<b>Hello</b>");
```
```javascript 
// Get an attribute of an element
$("img").attr("src");
$("h1").attr("class"); // Get all classess added to an element
// Set an attribut to an element / all matching elements
$("a").attr("href", "www.google.com");
```
```javascript 
// Event Listeners
$("h1").click(function () {
    $("h1").css("color", "#010101");
});
// Selects all buttons
$("button").click(function () {
    $("h1").css("display", "none");
})
// Record all keydown
$(document).keypress(function (event) {
    console.log(event.key);
});
```
```javascript 
// Add html before/after something (outside the element)
$('h1').before("<button>Hi</button>");
$('h1').after("<button>Hi</button>");
// Prepend/Append something to an element (inside the element)
$('h1').prepend("<button>Hi</button>");
$('h1').append("<button>Hi</button>");
```
```javascript 
// Remove all
$("h1").remove();
```

### Animations

```javascript 
// Show/Hide
$("h1").show();
$("h1").hide();
// Toggle the display of an element
$("button").click(function () {
    $("h1").toggle();
});
// Show/Hide with grace
$("h1").fadeOut();
$("h1").fadeIn();
$("h1").fadeToggle();
$("h1").slideUp();
$("h1").slideDown();
$("h1").slideToggle();
```
```javascript 
// Custom animation
$("button").click(function () {
    $("h1").animate({
        // Can only add css rules that have a numeric value (number, percentage etc.)
        opacity: 0.5
    });
});
```
```javascript 
// Combining animations
$("button").click(function () {
    $("h1").slideUp().slideDown().animate({opacity: "40%"});
});
```
