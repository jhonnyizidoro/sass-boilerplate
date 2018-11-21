
Global
=======

This is the file where I like to write my generic Sass for some elements. Like titles and subtitles. These styles will normally be used in the whole project.

Normalize
======
This file is just to fix some elements native styles in browsers.

App
=======

This is the main file, where you are going to `@import` all the other files. This is important because normally you are going to use a tool to proccess your Sass based in just one file.

Variables
=======

### RESPONSIVENESS
If tou access the **`_variables.scss`** file you will see six very important variables that has to do with the container and the responsiveness of your project. The most important of them is the **`$desktopStart`** variable. This variable defines in what point the columns will stack and the screen will be considered mobile. Then you will see a variable named **`$desktopContainer`**,  this is the size of the container in screens with the width between **`$desktopStart`** and **`$widescreenStart`**, after that, the screen will have the **`$widescreenContainer`** size and so on, until the **`$fullhdContainer`**. This variables are based on the [Bulma's](http://localhost/) variables.

### These are the default values, feel free to change them.

Screen Sizes  				|Container Sizes
----------------------------|--------------------
`smaller then $desktopStart`|`100%`
`$desktopStart: 1000px`  	|`$desktopContainer: 1000px`
`$widescreenStart: 1280px`  |`$desktopContainer: 1152px`
`$fullHdStart: 1472px`  	|`$desktopContainer: 1344px`
****
### GRID
The grid system is called **`columns`**, a name inspired by [Bulma](http://localhost/) (:

The **`$columns`** variable defines how mutch columns your grid system will have, as 
I think that 12 is not enougth some times, it's default value is 24 (because it's divisible by 3 and 4), but you can change it, the CSS classes are generatade dynamically.

The other variable used in the grid system is the **`$gap`**. This is the value of the columns padding.
****
### COLORS
The color variables are used in other files to generate some `background` and `text color` helper classes. Feel free to change these variables colors or create new ones, but It's important to keep the default color variables.

Container
======
The container class is a wrapper class to keep you content aray from the borders of the screen. On mobile screens it will have `100%` of the screen width.
```html
<div class="container">
	...
</div>
```

Columns
=======
In order to use the columns you must use a wrapper div with the class of `.columns`. After that, all the direct child elements of these div must be a `.column`. You have to tell what is the width of that column using the class `is-x`. So let's imagine that your `$columns` variable is set to **24**.
```html
<div class="columns">
	<div class="column is-24">
		A full width column
	</div>
	<div class="column is-12">
		A half width column is the other line
	</div>
	<div class="column is-12">
		A half width column is the other line
	</div>
</div>
```

The `.columns` has two modifiers
* **`.gapless`**: remove the padding of the `.colum` child elements.
* **`.is-centered`**: align the `.colum` children in the center of the screen.

Helpers
=======
Some helper classes are generated dinamically in the **`_helpers.sass`** file.

### TEXT AND BACKGROUND COLOR
For each default color in the **`_variables.sass`** file, these classes will be generated.

```css
.text-primary: {
	color: "primary color"
}
.background-primary: {
	background-color: "primary color"
}
```
If you want to generate these classes for your custom colors, just add your color to the **`$defaultColors`** list in the helpers file.
****

### MARGIN AND PADDING
The following values are available for margin and padding helpers:

**0**, **5**, **10**, **15**, **20**, **25**, **30**, **40**, **50**, **75**, **100** 

And for each of them you can use these helpers classes below.

Class name 	|Output
------------|--------------------
`.m-50` 	|`margin: 50px`
`.m-t-75`	|`margin-top: 75px`
`.m-r-100`	|`margin-right: 100px`
`.m-b-0`	|`margin-bottom: 0px`
`.m-l-10` 	|`margin-left: 10px`
`.p-50` 	|`padding: 50px`
`.p-t-75`	|`padding-top: 75px`
`.p-r-100`	|`padding-right: 100px`
`.p-b-0`	|`padding-bottom: 0px`
`.p-l-10` 	|`padding-left: 10px`
****

### KEEP IMAGE AND IFRAME ASPECT RATIO
You can keep an image or iframe aspect raio by adding the class `.keep-ratio` in the parent element, and then add the class with the ratio you want. Available ratios: **1by1**, **4by3**, **5by3** and **16by9**.

Your HTML code will be like this:
```html
<figure class="keep-ratio is-16by9">
	<img src="http://localhost/img.png">
</figure>
```
****

### OTHER HELPER CLASSES
Class name 			|What is the result?
--------------------|--------------------
`.fullwidth` 		|`width: 100%`
`.fullheight` 		|`height: 100%`
`.fill` 			|`height and width: 100%`
`.text-right` 		|`display block and align right`
`.text-left` 		|`display block and align left`
`.text-center` 		|`display block and align center`
`.text-justify` 	|`display block and justify`
`.relative` 		|`position: relative`
`.absolute` 		|`position: absolute`
`.fixed` 			|`position: fixed`
`.static` 			|`position: static`
`.hide-on-mobile` 	|`hide element on mobile devices`
`.hide-on-desktop` 	|`hide element on desktop devices`



Mixins
======
I thisnk this is the most cool and helpfull feature of Sass. It helps you to generate a lot of styles dinamically in just one line. Differently from the CSS classes, mixins are not set in the HTML, you must include them directly in the CSS, like the example bellow.
```css
/* Sass Syntax */
.class-name
	+mixin($paramenters)
/* SCSS Syntax */
.class-name {
	@include mixin($paramenters);
}
```
****
### MEDIA QUERIES MIXINS
To help our cause of writting the minimum of code we can and avoid repeating it, i created some media queries mixins. Use them like the example bellow.
```css
+mobile
	/* styles for desktop screens */
+desktop
	/* styles for desktop screens */
+widescreen
	/* styles for widescreen screens */
+fullhd
	/* styles for fullhd screens */
```
****
### FLEX MIXIN
This mixins recieves three parameters in the following order `justifiy-content`, `align-items`, `flex-direction` and `flex-wrap`.

>`flex-direction` is not required, it's default value is `row`.

>`flex-wrap` is not required, it's default value is `nowrap`.

```css
form.search
	+flex(space-between, center)
```
****
### COLUMNS MIXIN
With this mixin you can make a grid system in just onle line. This is my favorite one. And it makes