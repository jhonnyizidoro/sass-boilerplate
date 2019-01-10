# SASS Boilerplate
Hi, this is my default Sass boilerplate for my projects. Feel free to use it. You must know at least the basics about Sass to use it. This doc will cover file by file, in the order that they are imported in the **app.sass** file.
## Whay Sass, not SCSS?
The answer is simple, you write less code, a lot less and it's more productive. Take a simple use of a mixin as an example.
```scss
/** SCSS syntax */
.container {
  @include mixin_name($parameter);
}
/** Sass syntax */
.container
  +mixin_name($parameter)
```
## App
This is the main file, where all the other files will be imported. This is necessary because Sass processors normaly process only one file by default. The variables and mixins files must be the firsts to be included.
## Variables and Container
The **_variables.sass** file is the core of this boilerplate. You can customize any of the variables as you want. By default this boilerplate has 5 screen sizes. *Mobile*, *Tablet*, *Desktop*, *Widescreen* and *Full HD*. Every size has it's respective variables, except for the *mobile* size, wich is smaller than *tablet*.
```scss
$tabletStart: 600px
$tabletContainer: 100%

$desktopStart: 1024px
$desktopContainer: 100%

$widescreenStart: 1280px
$widescreenContainer: 1280px

$fullHdStart: 1472px
$fullHdContainer: 1344px
```
These two variables defines how mutch columns the grid system will have and how larger is the gap between the columns.
```scss
$columns: 24
$gap: 10px
```

The color variables are not that important, but is a good practice to don't use colors directly in your Sass files, always use clor variables.
## Mixins
This is my favorite Sass feature, this helps you to inject a lot of CSS with just one line os Sass. The best thing about mixins if that the mixin will only be proccessed if used, so you can have how mutch mixins you want. I will cover one by one.

### **+mobile / +desktop / +widescreen / +fullhd**

Use these mixins when you need to stylize and element for just one screen size. Normally you will just stylize an element and after use the **mobile** and **tablet** mixin for some adjusts. Just remember that this mixins will use the responsiveness variables as parmeter.

```css
/* USAGE */
+desktop
  .container
    background-color: blue
+mobile
  .container
    background-color: red

/* OUTPUT */
@media only screen and (min-width: 1024px) {
  .container {
    background-color: blue;
  }
}
@media only screen and (max-width: 600px) {
  .container {
    background-color: red;
  }
}
```
### **+flex**
Parameters: $justify **REQUIRED**, $align **REQUIRED**, $direction *DEFAULT row*, $wrap *DEFAULT nowrap*, $grow *DEFAULT 0*, $shrink *DEFAULT 1*
```css
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
### **+columns**
This will generate a system like the grid system, but only for the element that you apply this mixin. The cool thing about this is that it allows you to change how mutch columns you will have in mobile, tablet and desktop. The first parameter is the $totalColumns. If you pass 4, for example, all the direct children of thre element will have 25% width.

Parameters: $totalColumns **REQUIRED**, $gap *DEFAULT $gap*
```css
/* USAGE */
.container
  +columns(4)

+tablet
  .container
    +columns(2)

+mobile
  .container
    +columns(1)

/* OUTPUT */
@media only screen and (min-width: 1024px) {
  .container {
    flex-direction: row;
    display: flex;
    flex-wrap: wrap;
  }
  .container > * {
    padding: 10px;
    width: 25%;
  }
}
@media only screen and (max-width: 1023px) {
  .container {
    flex-direction: row;
    display: flex;
    flex-wrap: wrap;
  }
  .container > * {
    padding: 0;
    width: 50%;
  }
}
@media only screen and (max-width: 600px) {
  .container {
    flex-direction: row;
    display: flex;
    flex-wrap: wrap;
  }
  .container > * {
    padding: 0;
    width: 100%;
  }
}
```
### **+font**
This is other mixins that can make your Sass a lot cleaner. All the parameters are optionals. I made the variables name with only one letter, it seems to be confusing in the beginning, but once you are used to it, it's very easier.

Parameters: $s: *font-size*, $w: *font-weight*, $lh: *line-height*, $c: *color*, $t: *text-transform*, $a: *text-align*, $ls: *letter-spacing*
```css
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
### **+cover**
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
### **centralizeY**
This mixin should be used in the parent element, than you should pass the selector of the element that will be centralized as a parameter.

Parameters: $chilElement **REQUIRED**, $width *DEFAULT 100%*, $parentPosition *DEFAULT relative*
```css
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
### **+size**
Defines the size of the element. If you pass only one parameter, both width and height will have the sabe size, but you can pass the width and height two.

Parameters: $width **REQUIRED**, $height *DEFAULT $width*
```css
/* USAGE */
.container
  +size(20px)

/* OUTPUT */
.container {
  width: 20px;
  height: 20px;
}
```
### **+position**
If the **$position** parameter is *false*, the mixin won't change the element position.

Parameters: $t *DEFAULT auto*, $r *DEFAULT auto*, $b *DEFAULT auto*, $l *DEFAULT auto*, $position *DEFAULT absolute*
```css
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
### **+border**
Parameters: $style **REQUIRED**, $sides **REQUIRED _[top, right, bottom or left]_**
```css
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
### **+pseudo**
Parameters: $display *DEFAULT block*, $position *DEFAULT absolute*, $content *DEFAULT ' '*
```css
/* USAGE */
.container::after
  +pseudo

/* OUTPUT */
.container::after {
  content: '';
  position: absolute;
  display: block;
}
```
### **+background**
All these parameters are optionals. The property won't be changed if you don't pass the parameter to the mixin.

Parameters: $image: *background-image*, $repeat: *background-repeat*, $color: *background-color*, $origin: *background-origin*, $cover: *background-cover*, $position: *background-position*
```css
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