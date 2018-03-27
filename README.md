# Foundations Session 8

## Homework

Start on your final projects. There are very few requirements for this project other than it must be a web page or series of web pages that incorporate the concepts and techniques covered in class.

It is not required that you prepare a specific number of pages. Depending on the design goals, one good template could suffice for many pages and it is possible to spend as much time on a single page as on an entire site.

Making the page "mobile friendly" is required as is at least one instance of DOM scripting.


Top of the page

![image](/img/wide.png)

Mobile view

![image](/img/mobile.png)

Full page

![image](/img/siteDesign.png) 

Review the structure of the page using the mini version.

```css
nav ul {
	display: flex;
	justify-content: space-around;
	background: #ddd;
}

img, iframe {
	width: 100%;
}

ul {
	list-style: none;
	padding: 0;
}

iframe {
	background-color: #000;
}

header {
	max-width: 980px;
	margin: 0 auto;
}

section {
	display: flex;
	max-width: 980px;
	margin: 0 auto;
	border: 4px solid red;
}

article {
	flex: 2;
	padding-right: 2rem;
	background: #eee;
}

aside {
	flex: 1;
	background: #ddd;
}

footer .siteinfo {
	display: flex;
	max-width: 980px;
	margin: 0 auto;
}

.siteinfo > * {
	flex: 1;
}
```

Add responsive code for the main columns.

```css
@media (max-width: 420px) {
	nav ul {
		flex-direction: column;
	}
	section {
		display: block;
	}
	article {
		padding-right: 0;
	}
	footer .siteinfo {
		display: block;
	}
}
```


## Tooling

Windows users - for browser sync you must escape `\"` the `'`  characters in the package.json file, e.g.:

```js
"scripts": {
   "startmac": "browser-sync start --browser \"chrome\" --server \"app\" --files \"app\"",
   "startpc": "browser-sync start --browser \"chrome\" --server \"definition-list\" --files \"definition-list\""
 },
```

```sh
$ cd <session8>
$ npm install
$ npm run boom!
```

Review: 

* directory structure
* header nesting .css to .scss
* sass mapping
* Media Query - Mobile First
* Variables
* Responsive Nav .scss

Add variables:

```
$max-width: 940px;

$break-sm: 480px;
$break-med: 768px;

$radius: 4px;

$link: #4e7c92;
$hover: #df3030;
$text: #333;

$med-gray: #666;
$light-gray: #ddd;
$dk-yellow: #dbd1b5;
$lt-yellow: #f8f7f3;
```


### Responsive Images

iFrame and images need to expand and contract to fit. 

Note the inline width and height parameters for the iFrame in the HTML.

_base.scss:

```css
img,
iframe {
  width: 100%;
}
```

Also add some basic styling to _base.scss:

```css
p {
	margin: 12px 0;
}

h2 {
	margin-bottom: 12px;
	padding-bottom: 6px;
	font-size: 24px;
	letter-spacing: -1px;
}

h3, h4 {
	font-size: 16px;
	line-height: 1.25;
	margin-bottom: 20px;
}
```

## Sticky Nav

In `_nav.scss`:

```css
nav {
	position: fixed;
	width: 100%;
	🔥
}
```

Add padding to the top of the header to compensate.

Add black color to the video iframe.


## Columns for Content

Review the html structure of the page.

In a new _structure.scss file:

```css
section {
	max-width: 940px;
	margin: 0 auto;
	padding-bottom: 1.5em;
}
article {
 	box-sizing: border-box;
	float: left;
	width: 60%;
	padding-right: 24px;
}
aside {
	float: right;
	width: 40%;
}
```

Apply the second breakpoint variable to medium screen sizes and above only:

```css
@media (min-width: $break-med) {
	section {
		max-width: 940px;
		margin: 0 auto;
		padding-bottom: 1.5em;
	}
	article {
		box-sizing: border-box;
		float: left;
		width: 60%;
		padding-right: 24px;
	}
	aside {
		float: right;
		width: 40%;
	}
}
```

The Secondary div:

```css
.secondary {
	background: $lt-yellow;
	border:1px solid $dk-yellow;
	padding:1em;
}
```

### Micro clearfix

```css
section:before,
section:after {
    content: " ";
    display: table;
}
section:after {
    clear: both;
}
```

If you use this approach it is best to define a cf class and use it as necessary.

```css
.clearfix:before,
.clearfix:after {
    content: " ";
    display: table;
}
.clearfix:after {
    clear: both;
}
```

Add the clearfix to the section and secondary div:

`<section class="clearfix">`

`<div class="secondary clearfix">`


### Flex Columns

```css
@media (min-width: $break-sm) {
	section {
		max-width: 940px;
		margin: 0 auto;
		display: flex;
	}
	article {
		flex: 2;
		padding-right: 2rem;
	}
	aside {
		flex: 1;
	}
}

.secondary {
	background: $lt-yellow;
	border:1px solid $dk-yellow;
	padding:1em;
}
```


### CSS Grid

Delete/comment everything from _structure.scss except the .secondary rule.

```css
section {
	max-width: $max-width;
	margin: 0 auto;
	display: grid;
	grid-template-columns: 60% 40%;
	grid-column-gap: 2rem;
}
```

Note that, because of the column gap, the overall width of the two columns is greater than 100%.

Use `fr` units instead to keep proportion and allow a gap that is contained by the overall max-width:

```css
section {
	max-width: $max-width;
	margin: 0 auto;
	display: grid;
	grid-template-columns: 8fr 4fr;
	grid-column-gap: 2rem;
}
```

### The Footer 

Examine the html structure for this section.

Import a new file `_footer.scss` in styles.scss and add:

```css
footer {
	margin-top: 40px;
	padding-top: 40px; 
	background-color: $link;
	min-height: 320px;
	.siteinfo {
		display: grid;
		grid-template-columns: 6fr 3fr 3fr;
		grid-column-gap: 4rem;
		max-width: $max-width;
		margin: 0 auto;
		color: #fff;
		a {
			color: #fff;
		}
		p {
			margin-top: 0;
		}
	}
}
```

Test on large and small screens.

### Video Switcher - JavaScript

Active class

Format the video buttons

```css
.btn-list {
	padding: 6px;
	display: flex;
	li {
		margin-right: 18px;
		margin-bottom: 16px;
	}
	.active {
		border-radius: $radius;
		background: $link;
		color: #fff;
		padding: 0.5rem;
	}
}
```

Create variables and spread the links into an array.

```js
const videoLinks = document.querySelectorAll('.content-video a');
videoLinks.forEach( videoLink => videoLink.addEventListener('click', selectVideo ));
```

Examine the nodelist in the console.

Add the `selectVideo` function:

```js
const videoLinks = document.querySelectorAll('.content-video a');
videoLinks.forEach( videoLink => videoLink.addEventListener('click', selectVideo ));

function selectVideo(){
	console.log(this)
	event.preventDefault()
}
```

Examine the nodelist in the console.

```js
function selectVideo(){
	const videoToPlay = this.getAttribute('href')
	console.log(videoToPlay)
	event.preventDefault()
}
```

Add the iFrame variable `const iFrame = document.querySelector('iframe')` and set its src attribute `iFrame.setAttribute('src', videoToPlay)`:

```js
const iFrame = document.querySelector('iframe') // NEW
const videoLinks = document.querySelectorAll('.content-video a');
videoLinks.forEach( videoLink => videoLink.addEventListener('click', selectVideo ));

function selectVideo(){
	const videoToPlay = this.getAttribute('href')
	iFrame.setAttribute('src', videoToPlay)
	console.log(iFrame) // NEW
	event.preventDefault()
}
```

Switch the active class:

```js
const iFrame = document.querySelector('iframe') // NEW
const videoLinks = document.querySelectorAll('.content-video a');
videoLinks.forEach( videoLink => videoLink.addEventListener('click', selectVideo ));

function selectVideo(){
	removeActiveClass()
	this.classList.add('active')
	const videoToPlay = this.getAttribute('href')
	iFrame.setAttribute('src', videoToPlay)
	event.preventDefault()
}

function removeActiveClass(){
	videoLinks.forEach( videoLink => videoLink.classList.remove('active'))
}
```

# Start of session 9

### Nav Sub

Integrate the JavaScript for nav-sub into the layout.

in _navsub.scss:

```css
.nav-sub {
	padding: 10px 20px;
	background-color: $lt-yellow;
	border: 1px solid $dk-yellow;
	@media (min-width: $break-med){
		width: 40%;
		float: right;
		border-radius: $radius;
		margin: 0;
		float: none;
		width: auto;
	}
	ul {
		display:none;
	}
	li:first-child ul {
		display:block;
	}
	> li > a { 
		font-weight:bold; 
	}
	ul li {
		padding-left:12px;
	}
}
```

Note the `>` [selector](https://www.w3schools.com/cssref/css_selectors.asp). Also see [Combinators](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Simple_selectors)

Add class `.active {display: block !important}` to _nav-sub.scss:

```css
.nav-sub {
	padding: 10px 20px;
	background-color: $lt-yellow;
	border: 1px solid $dk-yellow;
	@media (min-width: $break-med){
		width: 40%;
		float: right;
		border-radius: $radius;
		margin: 0;
		float: none;
		width: auto;
	}
	ul {
		display:none;
	}
	li:first-child ul {
		display:block;
	}
	> li > a { 
		font-weight:bold; 
	}
	ul li {
		padding-left:12px;
	}
	.active {display: block !important}
}

```

Accordion for Nav Sub. 

Old school JavaScript:

```js
$('.nav-sub>li a').on('click tap', function(){
	$('.nav-sub ul').slideUp();
	$(this).next().slideToggle();
	console.log(this);
	return false;
});
```

ES6 JavaScript. 

```
const subnavLinks = document.querySelectorAll('.nav-sub > li a')
console.log(subnavLinks)
const subnavLinksArray = [...subnavLinks]
subnavLinksArray.forEach( subnavLink => subnavLink.addEventListener('click', openAccordion))

function openAccordion(){
	console.log(this)
	event.preventDefault()
}
```

[DOM Traversal](https://www.w3schools.com/jsref/dom_obj_document.asp)

nextElementSibling, nextSibling, previousSibling, childNodes, firstChild ...

```
const subnavLinks = document.querySelectorAll('.nav-sub > li > a')
const subnavLinksArray = [...subnavLinks]
subnavLinksArray.forEach( subnavLink => subnavLink.addEventListener('click', openAccordion))

function openAccordion(){
	this.nextElementSibling.classList.toggle('active')
	event.preventDefault()
}
```

Remove the active class from the DOM before applying with `removeActiveClass()`:

```
const subnavLinks = document.querySelectorAll('.nav-sub > li > a')
const subnavLinksArray = [...subnavLinks]
subnavLinksArray.forEach( subnavLink => subnavLink.addEventListener('click', openAccordion))

function openAccordion(){
	removeActiveClass()
	this.nextElementSibling.classList.toggle('active')
	event.preventDefault()
}

function removeActiveClass(){
	subnavLinksArray.forEach( subnavLink => subnavLink.nextElementSibling.classList.remove('active'))
}
```

Important - we have broken the removeActiveClass() function for the video switcher.

Set the initial state of the accordion with: `subnavLinksArray[0].nextElementSibling.classList.add('active')`

```
const subnavLinks = document.querySelectorAll('.nav-sub > li > a')
const subnavLinksArray = [...subnavLinks]
subnavLinksArray.forEach( subnavLink => subnavLink.addEventListener('click', openAccordion))
subnavLinksArray[0].nextElementSibling.classList.add('active')

function openAccordion(){
	removeActiveClass()
	this.nextElementSibling.classList.toggle('active')
	event.preventDefault()
}

function removeActiveClass(){
	subnavLinksArray.forEach( subnavLink => subnavLink.nextElementSibling.classList.remove('active'))
}
```

and remove the css created earlier:

```
	// li:first-child ul {
	// 	display:block;
	// }
```

Note the refresh behaviour.

Note the lack of animation.


### Image Carousel 

Do a DOM review of this section of the page.

In _carousel.scss:

```css
.secondary aside {
	ul {
		display: flex;
		flex-wrap: wrap;
		align-content: space-around;
		li {
			margin: 6px;
		}
		li img {
			width: 80px;
			padding: 10px;
			background-color: #fff;
			border: 1px solid $lt-yellow;
			transition: all 0.2s linear;
			&:hover {
				transform: scale(1.1);
				box-shadow: 1px 1px 1px rgba(0,0,0,0.4);
			}
		}
	}
}
```

Note transition:

```css
li img {
	...
	transition: all 0.2s linear;
	&:hover {
		transform: scale(1.1);
		box-shadow: 1px 1px 1px rgba(0,0,0,0.4);
	}
```

Content Slider - examine image

```css
figure {
	position: relative;
	figcaption {
		padding: 6px;
		background: rgba(255,255,255,0.7);
		position: absolute;
		bottom: 0;
	}
}	
```

### Image Carousel - JavaScript

change the # links to point to high res images:

```
<ul class="image-tn">
  <li>
    <a href="img/bamboo.jpg"><img src="img/bamboo-tn.jpg" alt="" title="Link to original photo on Flickr" /></a>
  </li>
  <li>
    <a href="img/bridge.jpg"><img src="img/bridge-tn.jpg" alt="" title="Link to original photo on Flickr" /></a>
  </li>
  <li>
    <a href="img/pagoda.jpg"><img src="img/pagoda-tn.jpg" alt="" title="Link to original photo on Flickr" /></a>
  </li>
```

Old school JavaScript:

```js
$('.image-tn a').on('click tap', function(){
    var imgsrc = $(this).attr('href');
    var titleText = $(this).find('img').attr('title');
    $('figure > img').attr('src', imgsrc);
    $('figcaption').html(titleText);
    return false;
});
```

```
const carouselLinks = document.querySelectorAll('.image-tn a')
const carouselLinksArray = [...carouselLinks]
const carousel = document.querySelector('figure img')

carouselLinksArray.forEach( carouselLink => carouselLink.addEventListener('click', runCarousel ))

function runCarousel(){
	const imageHref = this.getAttribute('href')
	carousel.setAttribute('src', imageHref)
	event.preventDefault()
}
```

Set the text in the carousel.

Find the appropriate traversal `const titleText = this.firstChild.title`:

```
function runCarousel(){
	const imageHref = this.getAttribute('href')
	const titleText = this.firstChild.title
	console.log(titleText)
	carousel.setAttribute('src', imageHref)
	event.preventDefault()
}
```

Create a pointer to the figcaption in order to manipulate its content:

```
const carouselPara = document.querySelector('figcaption')
```

Set the innerHTML `carouselPara.innerHTML = titleText` of the paragraph:

```
function runCarousel(){
	const imageHref = this.getAttribute('href')
	const titleText = this.firstChild.title
	carouselPara.innerHTML = titleText
	console.log(carouselPara)
	carousel.setAttribute('src', imageHref)
	event.preventDefault()
}
```

Final script:

```
const carouselLinks = document.querySelectorAll('.image-tn a')
const carouselLinksArray = [...carouselLinks]
const carousel = document.querySelector('figure > img')
const carouselPara = document.querySelector('figcaption')
carouselLinksArray.forEach( carouselLink => carouselLink.addEventListener('click', runCarousel ))

function runCarousel(){
	const imageHref = this.getAttribute('href')
	const titleText = this.firstChild.title
	carouselPara.innerHTML = titleText
	carousel.setAttribute('src', imageHref)
	event.preventDefault()
}
```



### The Panels (the third and final section)

Review the design. Let's try floats and absolute/relative positioning.

In _panels.scss:

```css
.hentry {
  position: relative;
  float: left;
  width: 50%;
}
```

The little date area

```css
.hentry {
	position: relative;
	float: left;
	box-sizing: border-box;
	width: 50%;
	padding: 1rem;
	.published {
		position: absolute;
		top: 250px;
		left: 1rem;
		display: block;
		width: 30px;
		padding: 5px 10px;
		background-color: $link;
		font-size: 10px;
		text-align: center;
		text-transform: uppercase;
		color: #fff;
	}
	.day {
		font-size: 32px;
	}
	h4 {
		margin: 0 0 10px 60px;
		font-size: 20px;
	}
	p {
		margin-left: 60px;
	}
}
```

Parent container .hentries is used here.

Adding abbr formatting, removing positioning and using flexbox and floats.

```css
.hentries {
	display: flex;
	abbr {
		text-decoration: none;
		text-align: center;
	}
	.hentry {
		float: left;
		box-sizing: border-box;
		width: 50%;
		padding: 1rem;
		.published {
			float: left;
			width: 24%;
			box-sizing: border-box;
		// position: absolute;
		// top: 250px;
		// left: 1rem;
		display: block;
		// width: 50px;
		padding: 5px 10px;
		background-color: $link;
		font-size: 10px;
		text-align: center;
		text-transform: uppercase;
		color: #fff;
	}
	.day {
		font-size: 32px;
	}
	h4 {
		// margin: 0 0 10px 60px;
		font-size: 20px;
	}
	p {
		// margin-left: 60px;
		margin-top: 0;
		float: right;
		width: 70%;
		box-sizing: border-box;
	}
}
}
```

Final _panels.scss:

```
.hentries {
	display: flex;
	abbr {
		text-decoration: none;
	}
	.hentry {
		float: left;
		box-sizing: border-box;
		width: 50%;
		padding: 0 8px;
		.published {
			text-align: center;
			float: left;
			width: 24%;
			box-sizing: border-box;
			display: block;
			padding: 2px 6px;
			background-color: $link;
			font-size: 10px;
			text-align: center;
			text-transform: uppercase;
			color: #fff;
		}
		.day {
			font-size: 32px;
		}
		h4 {
			font-size: 20px;
		}
		p {
			margin-top: 0;
			float: right;
			width: 70%;
			box-sizing: border-box;
		}
	}
}
```

Note RSS feed attribute selectors

```css
a[rel="alternate"] {
	padding-left: 20px;
	background: url(../img/a-rss.png) no-repeat 0 50%;
}
```

with svg:

```css
a[rel="alternate"] {
	padding-left: 20px;
	background: url(../img/feed-icon.svg) no-repeat 0 50%;
    background-size: contain;
}
```



## Notes

```js
{
  "name": "session7",
  "version": "1.0.0",
  "description": "## Homework",
  "main": "index.js",
  "scripts": {
    "sassy": "node-sass --watch sass --output app/css --source-map true",
    "start": "browser-sync start --server 'app' --files 'app'",
    "boom!": "concurrently \"npm run start\" \"npm run sassy\" "
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/front-end-foundations/session7.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/front-end-foundations/session7/issues"
  },
  "homepage": "https://github.com/front-end-foundations/session7#readme",
  "devDependencies": {
    "browser-sync": "^2.18.13",
    "concurrently": "^3.5.0",
    "node-sass": "^4.6.0"
  }
}
```

### Links

`<li><a href="#two">Summary</a></li>`

`<div class="secondary" id="two">`

```
html {
  scroll-behavior: smooth;
}
```

https://www.sitepoint.com/smooth-scrolling-vanilla-javascript/

```
initSmoothScrolling();

function initSmoothScrolling() {
  if (isCssSmoothSCrollSupported()) {
    return;
  }

  var duration = 400;

  var pageUrl = location.hash ?
    stripHash(location.href) :
    location.href;

  delegatedLinkHijacking();
  //directLinkHijacking();

  function delegatedLinkHijacking() {
    document.body.addEventListener('click', onClick, false);

    function onClick(e) {
      if (!isInPageLink(e.target))
        return;

      e.stopPropagation();
      e.preventDefault();

      jump(e.target.hash, {
        duration: duration,
        callback: function() {
          setFocus(e.target.hash);
        }
      });
    }
  }

  function directLinkHijacking() {
    [].slice.call(document.querySelectorAll('a'))
      .filter(isInPageLink)
      .forEach(function(a) {
        a.addEventListener('click', onClick, false);
      });

    function onClick(e) {
      e.stopPropagation();
      e.preventDefault();

      jump(e.target.hash, {
        duration: duration,
      });
    }

  }

  function isInPageLink(n) {
    return n.tagName.toLowerCase() === 'a' &&
      n.hash.length > 0 &&
      stripHash(n.href) === pageUrl;
  }

  function stripHash(url) {
    return url.slice(0, url.lastIndexOf('#'));
  }

  function isCssSmoothSCrollSupported() {
    return 'scrollBehavior' in document.documentElement.style;
  }

  // Adapted from:
  // https://www.nczonline.net/blog/2013/01/15/fixing-skip-to-content-links/
  function setFocus(hash) {
    var element = document.getElementById(hash.substring(1));

    if (element) {
      if (!/^(?:a|select|input|button|textarea)$/i.test(element.tagName)) {
        element.tabIndex = -1;
      }

      element.focus();
    }
  }

}

function jump(target, options) {
  var
    start = window.pageYOffset,
    opt = {
      duration: options.duration,
      offset: options.offset || 0,
      callback: options.callback,
      easing: options.easing || easeInOutQuad
    },
    distance = typeof target === 'string' ?
    opt.offset + document.querySelector(target).getBoundingClientRect().top :
    target,
    duration = typeof opt.duration === 'function' ?
    opt.duration(distance) :
    opt.duration,
    timeStart, timeElapsed;

  requestAnimationFrame(function(time) {
    timeStart = time;
    loop(time);
  });

  function loop(time) {
    timeElapsed = time - timeStart;

    window.scrollTo(0, opt.easing(timeElapsed, start, distance, duration));

    if (timeElapsed < duration)
      requestAnimationFrame(loop)
    else
      end();
  }

  function end() {
    window.scrollTo(0, start + distance);

    if (typeof opt.callback === 'function')
      opt.callback();
  }

  // Robert Penner's easeInOutQuad - http://robertpenner.com/easing/
  function easeInOutQuad(t, b, c, d) {
    t /= d / 2
    if (t < 1) return c / 2 * t * t + b
    t--
    return -c / 2 * (t * (t - 2) - 1) + b
  }

}






```



Additional Tweaks for Mobile (need to test on phone)

the tap event in JS

```js
$('.image-tn a').on('click tap', function(){
    var imgsrc = $(this).attr('href');
    var titleText = $(this).find('img').attr('title');
    $('.content-slider > img').attr('src',imgsrc);
    $('.caption').html(titleText);
    return false;
});
```

the z-index for images and navbar

```css
nav {
	height: 40px;
	width:100%;
	background: $link;
	font-size: 1rem;
	position: fixed;
	z-index: 20;
	top: 0;
```

media queries for transform effects (on hover)

```css
.secondary .content-sub {
	li {
		float: left;
		width: 33.333%;
		padding: 10px;
	}

	li img {
		padding: 10px;
		background-color: #fff;
		border: 1px solid #bfbfbf;
		border-bottom-color: #7c7c7a;
		width: 100%;
		height: auto;
		@media (min-width: $breakpoint-med){
			transition: all 0.2s linear;
			&:hover {
				-webkit-transform: scale(1.1);
				transform: scale(1.1);
				box-shadow: 1px 1px 4px rgba(0,0,0,0.4);
			}
		}
	}
}
```














