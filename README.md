Hi, this is my default Sass boilerplate for my projects. Feel free to use it. You must know at least the basics about Sass, or just read the docs (:

This doc will cover file by file, in the order that they are imported in the app.sass file.
## Whay Sass, not SCSS?
The answer is simple, you write less code, a lot less. It's more productive, take a simple use of a mixin as an example.

```scss
SCSS syntax
.container {
  @include mixin_name($parameter)
}

Sass syntax
.container
  +mixin_name($parameter)
```
## App
This is the mais file, where all the other files will be imported. This is necessary because Sass processors normaly process only one file by default. The variables and mixins files must be the firsts to be included.
## Variables and Container
The _variables file is the core of this boilerplate. You can customize any of them.

The $desktopStart variable defines the size where the columns will stack and your screen will be considered mobile. Then whe have the $desktopContainer, that defines the size of the container in screens larger than $desktopStart. The same rule is applied for $widscreenStart, in screens with the width between $widsecreenStart and $fullHdStart, the container size will be $widescreenContainer. In screen larger than $fullHdStart, the container size will always be $fullHdContainer.
```scss
$desktopStart: 1000px
$desktopContainer: 1000px

$widescreenStart: 1280px
$widescreenContainer: 1152px

$fullHdStart: 1472px
$fullHdContainer: 1344px
```

These two variables defines how mutch columns the grid system will have and how larger is the gap between the columns.
```scss
$columns: 24
$gap: 10px
```

The color variables are not that important, but you must keep the default ones because the _helpers file will use them to gerenerate some helper classes. I don't think it's necessary to create more colors, just customize the ones tha already existis.
## Mixins
This is my favorite feature of Sass, this helps you to inject a lot of CSS with just one line os Sass. I will cover one by one of the mixins bellow.

Mobile, desktop, widescreen and fullhd

Use these mixins when you need to stylize and element for just one screen size. Normally you will just stylize an element and after use the mobile mixin for some adjusts. Just remember that this mixins will use the responsiveness variables as parmeter.

```css
/* USAGE */
+desktop
  .container
    background-color: blue
+mobile
  .container
    background-color: red

/* OUTPUT */
@media only screen and (min-width: 1001px) {
  .container {
    background-color: blue;
  }
}
@media only screen and (max-width: 1000px) {
  .container {
    background-color: red;
  }
}
```
### Flex
This mixins receives six parameters, but some of them are not required, they are:
```css
/* PARAMETERS */
/* $justify REQUIRED */
/* $align REQUIRED */
/* $direction DEFAULT row */
/* $wrap DEFAULT nowrap */
/* $grow DEFAULT 0 */
/* $shrink DEFAULT 1 */

/* USAGE */
.container
  +flex(center, flex-start, $grow: 1)

/* OUTPUT */
.container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: row;
  flex-wrap: nowrap;
}
.container > * {
  flex-grow: 1;
  flex-shrink: 1;
}
```
### Columns
This will generate a system like the grid system, but only for the element that you apply this mixin. The cool thing about this is that it allows you to change how mutch columns you will have in mobile and desktop. The first parameter is the $totalColumns. If you pass 4, for example, all the direct children of thre element will have 25% width.
```css
/* PARAMETERS */
/* $totalColumns REQUIRED */
/* $gap DEFAULT $gap (set in the variables file) */
/* $mobile DEFAULT false */

/* USAGE */
.container
  +columns(4)
  +columns(2, 0, true)

/* OUTPUT */
@media only screen and (min-width: 1001px) {
  .container {
    display: flex;
    flex-wrap: wrap;
  }
  .container > * {
    padding: 10px;
    width: 25%;
  }
}
@media only screen and (max-width: 1000px) {
  .container {
    display: flex;
    flex-wrap: wrap;
  }
  .container > * {
    padding: 0;
    width: 50%;
  }
}
```
### Font
This is other mixins that can make your Sass a lot cleaner. All the parameters are optional. I made the variable name with only one letter, it seems to be confusing in the beginning, but once you are used to it, it's very easier.
```css
/* PARAMETERS */
/* $s: font-size */
/* $w: font-weight */
/* $lh: line-height */
/* $c: color */
/* $t: text-transform */
/* $a: text-align */
/* $ls: letter-spacing */

/* USAGE */
p.article
  +font(2rem, $c: red, $t: uppercase)

/* OUTPUT */
p.article {
  font-size: 2rem;
  color: red;
  text-transform: uppercase;
}
```
### Cover
Make you image cover the wrapper div.
```css
/* USAGE */
img
  +cover

/* OUTPUT */
img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```
### Centralize Y
This mixin should be used in the parent element, than you should pass the selector of the element that will be centralized as a parameter.
```css
/* PARAMETERS */
/* $chilElement REQUIRED */
/* $width DEFAULT 100% */
/* $parentPosition DEFAULT relative */

/* USAGE */
.container
  +centralizeY('nav.navbar')

/* OUTPUT */
.container {
  position: relative;
}
.container nav.navbar {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
}
```
### Size
Defines the size of the element. If you pass only one parameter, both width and height will have the sabe size, but you can pass the width and height two.
```css
/* PARAMETERS */
/* $width REQUIRED */
/* $height DEFAULT $width */

/* USAGE */
.container
  +size(20px)

/* OUTPUT */
.container {
  width: 20px;
  height: 20px;
}
```
### Position
Passa $position: false if you don't wanna change the element position.
```css
/* PARAMETERS */
/* $t DEFAULT auto */
/* $r DEFAULT auto */
/* $b DEFAULT auto */
/* $l DEFAULT auto */
/* $position DEFAULT absolute */

/* USAGE */
.container
  +position(10px, $l: 5px)

/* OUTPUT */
.container {
  position: absolute;
  top: 10px;
  left: 5px;
}
```
### Border
This is only useful if you wanna apply border in two or three sides, otherwise is bettrer to use the default CSS property.
```css
/* PARAMETERS */
/* $style REQUIRED [top, right, bottom or left] */
/* $sides REQUIRED */

/* USAGE */
.container
  +border(1px solid red, top, right, bottom)

/* OUTPUT */
.container {
  border-top: 1px solid red;
  border-right: 1px solid red;
  border-bottom: 1px solid red;
}
```
### Pseudo
I use this somethimes in pseudo elements (::befone and ::after), because almos always this propertys are default.
```css
/* PARAMETERS */
/* $display DEFAULT block */
/* $position DEFAULT absolute */
/* $content DEFAULT '' */

/* USAGE */
.container::after
  +pseudo

/* OUTPUT */
.container::after {
  content: '';
  display: block;
  position: absolute;
}
```
### Truncate
This is useful when you wanna truncate some text inside a block.
```css
/* PARAMETERS */
/* $maxWidth REQUIRED */
/* $display DEFUALT block */

/* USAGE */
h1
  +truncate(500px)

/* OUTPUT */
h1 {
  display: block;
  max-width: 500px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### Backgorund
This mixin is incomplete yet, I'm inserting parameters as long as I'm needing. Al these parameters are optional and will only be applied if passed to the mixin.
```css
/* PARAMETERS */
/* $image */
/* $repeat */
/* $color */
/* $origin */


/* USAGE */
body
  +background('/images/my-bg-img.jpg', no-repeat, $origin: 50% 50%)

/* OUTPUT */
body {
  background-image: url('/images/my-bg-img.jpg');
  background-repeat: no-repeat;
  background-origin: 50% 50%;
}
```

### Square
This is another mixin that need some improvement. Using this will generate a block with text somewhere in the div. Like the example bellow. You can pass center and center in the two first parameters, than the block will be centered in your div.
```css
/* PARAMETERS REQUIRED */
/* $top REQUIRED */
/* $background REQUIRED */
/* $color REQUIRED */
/* $text DEFAULT '' */


/* USAGE */
div
  +square(-10px, center, , #D52C2C, white, 'NOVO')

/* OUTPUT */
div {
  position: relative
}
div::after {
  padding: 0.25em 1em;
  content: 'NOVO';
  position: absolute;
  background: #D52C2C;
  color: white;
  right: 50%;
  transform: translateX(50%);
  top: -10px;
}
```
The output will be something like this:
![Square Mixin](https://i.imgur.com/LKAgl1r.png)