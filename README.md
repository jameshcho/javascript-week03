### Week 3: JavaScript syntax, variables, DOM

[Topics in Web Programming: JavaScript](https://github.com/ccny-edm/javascript)  
Instructor: Dan Phiffer ([dan@phiffer.org](mailto:dan@phiffer.org))

Now that we have HTML and CSS [figured out](https://github.com/ccny-edm/javascript-week02), we take on the third major technology of the web: JavaScript. You may recall that HTML defines the *structure* of a page, and CSS gives it a *visual appearance*. JavaScript is how we create the *behavior* of a web page.

*Start out this week's assignment without using copy and paste. Type very carefully!*

#### Part 1: Hello World

Let's start from a new HTML document. This should look familiar. Remember, you should type this in rather than using copy and paste.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Hello, World</title>
        <style>
    
        body {
            font: 18px/30px helvetica, sans-serif;
        }
    
        </style>
    </head>
    <body>
        Hello, World
    </body>
</html>
```

Save that to a file called 'hello.html' and use File > Open to load it in your browser. At each step, make sure you save your changes, and reload the page in your browser. Before continuing, [validate the page](http://validator.nu/) (choose 'file upload' instead of 'address') to make sure there are no problems out of the gate.

Our document has HTML, it has a little CSS, now let's add some JavaScript. Replace the page text in the body element with a `<script>` start tag, a `</script>` end tag, and one line of code in the middle.

```html
<body>
    <script>
    
    // Notify the world with your greeting
    alert('Hello, World');
    
    </script>
</body>
```

#### Part 2: Prompting the user

We now have an annoying pop-up introduction to an otherwise empty page. Let's tweak that slightly by adding a placeholder paragraph, and replacing the `alert` function call with `prompt`.

```html
<body>
    <p id="hello"></p>
    <script>
    
    // Make small talk with the user
    prompt('How are you today?');
    
    </script>
</body>
```

The page works pretty much as before—an annoying *interactive* pop-up introduction to an empty page. Let's do two things next: store the user's response to the `prompt` in a variable and then log that value to the Firebug console.

```html
<body>
    <p id="hello"></p>
    <script>
    
    // Store the user's response
    var response = prompt('How are you today?');
    
    // Log it to the Firebug console
    console.log(response);
    
    </script>
</body>
```

If you look at Firebug, you should see whatever you type into the pop-up repeated back to you in the console tab. Note the difference in what gets logged if you press 'OK' or 'Cancel'. For now let's just assume people will always press 'OK'.

#### Part 3: Modifying the page

Next, instead of logging the user's response to the Firebug console, we will insert it into the placeholder paragraph instead. Here is where we start needing the [Document Object Model](https://developer.mozilla.org/en-US/docs/DOM) (DOM). The first step is to get a reference to the paragraph using `getElementById` (note: capitalization matters).

```html
<body>
    <p id="hello"></p>
    <script>
    
    // Store the user's response
    var response = prompt('How are you today?');
    
    // Use the DOM to reference the paragraph above
    var hello = document.getElementById('hello');
    
    // Inspect the paragraph in Firebug
    console.log(hello);
    
    </script>
</body>
```

If all goes well, you should see `<p id="hello">` appear in your Firebug console. You can click on the logged element and inspect it within the HTML Firebug tab.

Now we will take the response from the user, and place it into the hello paragram we've referenced in JavaScript.

```html
<body>
    <p id="hello"></p>
    <script>
    
    // Store the user's response
    var response = prompt('How are you today?');
    
    // Use the DOM to reference the target
    var hello = document.getElementById('hello');
    
    // Replace the target's content with the user response
    hello.innerHTML = response;
    
    </script>
</body>
```

Now you should see what you type into the `prompt` pop-up appear on the page, within the placeholder paragraph. Use Firebug to inspect the paragraph: right click on it, then choose 'Inspect element with Firebug' (with the blue icon).

#### Part 4: Making Mad Libs

We now have enough technical understanding to make a [Mad Lib](http://en.wikipedia.org/wiki/Mad_Libs). Let's do it!

First, find some text as a starting point, something like 200-250 words is fine. You can use whatever you want as your source text; passages from [books](http://www.gutenberg.org/), [music lyrics](http://songmeanings.com/), [Wikipedia articles](http://en.wikipedia.org/wiki/Wikipedia:Featured_articles), go nuts. For the sake of demonstrating how this will work, let's start with the first sentence of Neil Stephenson's [In the Beginning Was the Command Line](http://www.cryptonomicon.com/beginning.html).

Go ahead and replace paragraph tag with your own text (copy and paste is okay now!), but following the pattern shown below:

```html
<body>
    <p>About twenty years ago Jobs and Wozniak, the founders of Apple, came up with the very strange
    idea of selling information processing machines for use in the home.</p>
```

Now pick out some words to replace, to create the placeholders for your Mad Lib. We will use `<span>` elements, each with a unique `id` attribute.

```html
<body>
    <p>About <span id="number">(number)</span> years ago <span id="name-1">(name)</span> and
    <span id="name-2">(name)</span>, the founders of <span id="company">(company)</span>, came
    up with the very strange idea of selling <span id="noun">(noun)</span> for use in the
    <span id="place">(place)</span>.</p>
```

Notice each `id` attribute is unique—if there are more than one "name" or "noun" replacements, just add a number to distinguish between them.

Let's create some JavaScript to insert a word replacement into the first placeholder span. It works just like our earlier experiments, so you can start by tweaking what you already have between your `<script>` tags.

```html
<script>

// Store the user's response
var response = prompt('Enter a number');

// Use the DOM to reference the paragraph above
var target = document.getElementById('number');

// Replace the target's content with the user response
target.innerHTML = response;

</script>
```

Now when you load the page, you should be able to modify the text using the same JavaScript prompt.

Since we are going to have a bunch of these, let's shorten that code down to a single line.

```html
<script>

document.getElementById('number').innerHTML = prompt('Enter a number');

</script>
```

This code is slightly harder to read as a single line, but it will make the entire program a little easier to manage. At this point we are going to break the *no copy-paste* rule again to avoid a bunch of unnecessary typing. Maybe add some progress numbers to let the user know how far along they are in the process.

```html
<script>

document.getElementById('number').innerHTML  = prompt('[1/6] Enter a number');
document.getElementById('name-1').innerHTML  = prompt('[2/6] Enter a name');
document.getElementById('name-2').innerHTML  = prompt('[3/6] Enter a name');
document.getElementById('company').innerHTML = prompt('[4/6] Enter a company');
document.getElementById('noun').innerHTML    = prompt('[5/6] Enter a noun');
document.getElementById('place').innerHTML   = prompt('[6/6] Enter a place');

</script>
```

One last detail, before we decide we're done with our Mad Lib—let's add some CSS to call attention to the replacements.

```
<style>

body {
    font: 18px/30px helvetica, sans-serif;
}

span {
    background: #ff9;
}

</style>
```

Here is how our finished example should look. Yours will not be exactly the same, of course, since your text and replacements are different. But the pattern should look similar.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>In the beginning...</title>
        <style>
    
        body {
            font: 18px/30px helvetica, sans-serif;
        }
        
        span {
            background: #ff9;
        }
    
        </style>
    </head>
    <body>
        <p>About <span id="number">(number)</span> years ago <span id="name-1">(name)</span>
        and <span id="name-2">(name)</span>, the founders of <span id="company">(company)</span>,
        came up with the very strange idea of selling <span id="noun">(noun)</span> for use in
        the <span id="place">(place)</span>.</p>
        <script>
    
        document.getElementById('number').innerHTML  = prompt('[1/6] Enter a number');
        document.getElementById('name-1').innerHTML  = prompt('[2/6] Enter a name');
        document.getElementById('name-2').innerHTML  = prompt('[3/6] Enter a name');
        document.getElementById('company').innerHTML = prompt('[4/6] Enter a company');
        document.getElementById('noun').innerHTML  = prompt('[5/6] Enter a noun');
        document.getElementById('place').innerHTML  = prompt('[6/6] Enter a place');
        
        </script>
    </body>
</html>
```
