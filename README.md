# Guidelines HTML
<sup>(v. 0.0.9)</sup>

These guidelines help to keep code clean, maintainable and scalable. 
Every point in here are high recommendations. 

Use these guidelines as blueprint and adjust it to the needs of your project.  

## Coding principles
* Start with the structure for the mobile view first before you write code for larger views. 
* Keep accessibility in mind during coding (e.g. make sure the page is usable without mouse, the semantic is valid and images have alt- or title-values if it is relevant)

##  Coding Style
* The code should be lowercase: HTML element names, attributes, attributes values (except strings).
* Avoid trailing white spaces and add a new line at the end of files (diffs & SVN).
* Whenever possible, use no more than 80 characters pro code line. To avoid long code lines in HTML, please place each element attribute below the previous one and align them according to the first attribute in the list. The right angle bracket (">") of the opening tag should be placed on a new line, aligned according to the left angle bracket of the opening tag. 
* use the "data-"-prefix for all attributes that are no valid w3c-attributes.
* avoid empty DOM-Elements.

``` html
 <!-- Attributes alignment example -->
  
 <div
     class="gl-comp-stage owl-carousel gl-owl-theme"
     data-owl=""
     data-owl-items="1"
     data-owl-autoplay="true"
     data-owl-loop="true"
     data-owl-nav="true"
     data-owl-speed="8000"
     data-testid="glStageCarousel"
 >
     ...
 </div>
  
 <input
     type="text"
     class="form-control gl-search-box--field"
     id="glSearchTerm"
     name="glSearchTerm"
     placeholder="Enter your search here"
     data-searchsuggest="" 
     data-form-control-compact="" 
     data-testid="glSearchBoxField"
 />
```

## Separation of Concerns
* Separate structure (markup), presentation (styling) and behavior (scripting).
* Link as few style sheets and scripts as possible from documents and templates.
* Avoid generating markup in javascript files.
* Don’t use inline styling (exception: javascript generated style for visual effects).

## Encoding
* Use UTF-8 without BOM (check your editor settings too).
* Declare the character encoding in the head section of the HTML templates and documents.
* Use unicode characters as HTML Entities.

``` html
<head>
    <meta charset="utf-8">
</head>
```

## Document Type
* Use HTML5 doctype at the beginning of every HTML template and document to enforce standard mode in every browser. 

``` html
<!DOCTYPE html>
```

## Including style sheets and scripts
* Do not use type attributes for style sheets and scripts, HTML5 implies text/css and text/javascript as defaults.

``` html
<link href="stylesheet.min.css" rel="stylesheet">
 
<script src="jsfile.min.js"></script>
 
<script>
...
</script>
``` 

## Semantics

* Use HTML elements according to their semantic purpose.
    * Make sure to have a proper headline hiararchy.
    * Use &lt;a&gt; elements only for anchors. Don't use &lt;a&gt; elements for items that are not linked. An element should be a link only when on right click on that element the "Open link in new tab" option should be available.
    * Use &lt;p&gt; elements for paragraphs. Don’t use multiple &lt;br /&gt; elements to add distance between elements.
    * Use &lt;ul&gt;, &lt;ol&gt; or &lt;dl&gt; elements for list items instead of a group of &lt;div&gt; or &lt;p&gt; elements.
    * Make use of the HTML5 semantic elements (&lt;header&gt;, &lt;footer&gt;, &lt;main&gt;, &lt;nav&gt;, &lt;section&gt;, &lt;small&gt;, etc.).
* When deciding upon which HTML element to use, the right questions to ask yourself are "what doest this element means, which kind of functionality does it have?" and not "how does this element looks like?".
* Keep in mind the document outline.

## General Formatting
* Put every block element on a new line.
* Indent every child element of a block element.
* USE XHTML markup style, even in HTML5 documents (lowercase code, quotes around attribute values, close all elements that have content, quote boolean attributes). Do close all void elements according to the XHTML syntax (input, img, br, hr, etc).

``` html
select="selected"
``` 

## HTML Quotation Marks

* Use double quotation marks around attribute values.

``` html
<!-- Not recommended -->
<a class='gl-btn--primary' data-testid='gl-login-button'>
    Login
</a>
 
<!-- Recommended -->
<a class="gl-btn--primary" data-testid="gl-login-button">
    Login
</a>
``` 

## Comments
* Use comments to explain code as needed.
* A comment should describe the purpose and the context of the code (how a component works, architecture, limitations).
* Place comments above the code they describe.
* Mark todos adding a comment starting with the keyword TODO wrapped by square brackets. Best practice: Create a ticket in your tracker and add the ticket number to the comment.

``` html
<!-- [TODO (project-12345)]: refactor buttons -->
<a class="button-red">
    Add to cart
</a>
```

## Forms Autofill
* Use Autofill to enrich your forms structure and behavior.
* Works with Chrome and Safari

List of recommended values:
* https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill
* https://developers.google.com/web/updates/2015/06/checkout-faster-with-autofill

``` html
<input name="street" autocomplete="section-one shipping address-line1">
```

## Unit tests and selenium tests with data-testid
To identify an element in a test (e.g unit test or selenium tests by the QA-Team) add the attribute „data-testid“ with a meaningful value to the element in the DOM. \
This helps to separate testing-data from the structure (html) and layout (css). 

The values must not change and be uniquely identified. 

At a minimum all interactive DOM-Elements must have a data-testid attribute. 
* anchors
* Buttons
* Form-fields
* Every element with events like onChange, onClick, onKeyDown, onKeyUp etc.  

Hint: These elements can be validated with an additional ES-Lint Plugin: 
https://github.com/davidcalhoun/eslint-plugin-test-selectors


### data-testid value:
For the value use BEM notation to ensure a readable structure. 

"components-name__element--modifier" 

``` html
<button onClick="checkout.html" data-testid="header__go-to-checkout">
    Go to checkout
</button>

<form data-testid="contact">
	<label for="name">Name</label>
	<input type="text" id="name" data-testid="contact__name">
</form>

<a href="#" onmouseover="tootltip()" data-testid="address-form__help">Help</a>
<div id="tootltip" data-testid="address-form__tooltip-help">How to...</div>
```
