# Kalon CSS Guidelines

A set of rules regarding CSS and how to write it in order to:

- keep stylesheets maintainable
- keep code clean 
- keep CSS scalable
- unify coding style across developers

## Table of contents 

* [Preprocessor](#preprocessor)
* [Formating](#formating)
* [File structure](#file-structure)
* [Folder structure](#folder-structure)
* [Comments](#comments)
* [Creating a ruleset](#creating-a-ruleset)
* [Indenting](#indenting)
* [Naming convention](#naming-convention)
* [Nesting order](#nesting-order)
* [Properties order](#properties-order)



## Preprocessor

All projects will be built using SASS preprocessor http://sass-lang.com/

Depending on project needs Compass can be added http://compass-style.org/



## Formating 

- 120 character wide columns
- multi line CSS
- child selectors & properties will be indented by one (1) tab



## File structure

All projects will have 1 main SCSS file 

- main.scss will represent the table of contents of the current project
- main.scss will NOT contain actual styles 
- main.scss is composed of a series of includes representing all components & modules of the project
- contents of the file will be placed in the following order: 

```SCSS
/* —- Utils -— */

// list of includes from outside the app
// these files will be never changed by Kalon developers. 
// this category will include files such as:  reset.scss, box-sizing.scss, etc.

@import('utils/reset');
@import('utils/box-sizing');
@import('utils/pseudo-elements');



/* —- Tools -— */

// useful functions that will be used across the project
// we can have 3 types of functions: 
//		- Kalon wide
//		- project specific
//		- component specific (located inside the component file / folder)

@import('mixins/libs/grid');
@import('mixins/libs/responsive');
@import('mixins/projectName/icons');



/* —- Settings -— */

// Globally available variables and configs such as: colours, fonts, margins etc.  

@import('settings/variables');
@import('settings/typography');



/* -— Components -— */

// list of componets that will be found in the project 

@import('components/logo');
@import('components/dropdown');
@import('components/grid');



/* -— Modules -— */

// list of modules that will be found in the project
// each module can contain 1 ore more components 

@import('modules/search-box');
@import('modules/products-list');
@import('modules/products-item');
@import('modules/product-detail-box');



/* -— Pages -— */

// list of pages that will be found in the project

@import('pages/home-page');
@import('pages/products-page');
```

## Folder structure

Files will be grouped in the following order: 

```JS
/SASS/
	— main.scss
	/libs/
		— _reset.scss
		— _box-sizing.scss
		... 
	/mixins/
		/libs/
			— _grid.scss
			— _responsive.scss
			... 
		/prjectName/ 
			— _icons.scss
			... 
	/globals/
		— _variables.scss
		— _typography.scss
		... 
	/components/
		— _dropdown.scss
		— _logo.scss
		... 
	/modules/
		— _products-list.scss
		... 
	/pages/
		— home-page.scss
		...
```



## Comments 

Begin every new major section with a title:

```SCSS
/*------------------------------------*\
    #SECTION-TITLE
\*------------------------------------*/
```

or 

```SCSS
/* -- #SECTION-TITLE -- */
```

Use block comments in the following manner: 

```SCSS
/**
 * Block Comment with long description . 
 * keep it under 120 chars / row
 */
```

Use ``` // ``` for inline comment blocks (instead of ``` /* */ ```)

```SCSS
.selector { 
	color: #FFF;  // inline comment . keep it very short . under 40 chars
}
```



## Creating a ruleset 

- opening brace (``` { ```) on the same line as selector;
- a 'space' before opening brace (``` { ```)
- closing brace (``` } ```) on its own new line

```SCSS
.selector { 
	// styles
}
```

```PHP
#WRONG#
.selector
{
}
```

- each declaration on a new line 
- a ‘space’ before each property value 
- each declaration ends with ``` ; ```
- each declaration indented by one (1) tab
- do not use units after 0 unless they are required
- when linking to to a resource use single quotes ``` '' ```
- use shorthand properties where possible
- hex or rgba() for setting colors
- shorthand color codes are preferred ``` #xyx ```
- lowercase letters for naming colors ``` #xxx ``` (NOT: ```#XXX```)  
- only use ``` px ``` as measuring unit. (NO ```em rem pt```)

```SCSS
.selector { 
	display: block;
	color: #FFF;
	margin: 0 10px;
	background: url('image.url');
}
```

```PHP
#WRONG#
.selector { display: block; margin: 0px; }

.selector { 
	display: block; 
	color: #FFF; }
```

- always add unit after 0 (0s) when creating animations
- when handling multiple selectors, each selector will have a new line

```SCSS
.selector,
.other-selector { 
	color: #FFF;
}
```

```PHP
#WRONG#
.selector, .other-selector {
}
```

- complex properties should be broken on multiple lines

```SCSS
.selector {
	transform: 
		translateX(100px)
		translateY(200px)
		scale(1.2);
}
```

- don't bind ruleset to specific HTML elements unless you really have to.

```PHP
#WRONG#
ul.component {
}
```



## Indenting

- no nesting
- no more then 3 levels depth
- 1 empty row between each rulesets
- 3 empty rows between somewhat related rulesets

```SCSS
/*------------------------------------*\
    #MODULE
\*------------------------------------*/

.Module {}

.Module-title {}

.Module-body {}



/*------------------------------------*\
    #COMPONENT
\*------------------------------------*/

.Component {

    &.selected {}
}

.Component-body {}
```

Nesting functionality of SASS can be used in this cases:

A) targeting pseudo elements ```:before``` & ```:after```

```SCSS
.Selector {
	display: block;

	&:before,
	&:after {
		content: '';
	}
}
```


B) targeting current component state 

```SCSS
.Selector {

	&.active {
		color: #F00;
	}
}
```

C) changing behaviour of component within module

```SCSS
.Module {

	.Component {
		display: block;
	}
}
```




## Naming convention

BEM like naming methodology will be used 

**Block** (e.g.: ``` navigation ```) 
**Element** (e.g.: ``` item ```)
**Modifier** (e.g.: ``` active ```)


- both components & modules are considered blocks in default behaviour
- a component can be considered as 'element' when used within a module
- CamelCase will be used for naming components 


```SCSS
.ComponentName { ... }

.ComponentName-subComponent { ... }
```

```PHP
#WRONG# 
.component { ... }
.component > .item { ... }
.component > .item.active { ... }
```

- avoid creating complex components

```PHP
#WRONG# 
.ComponentName-subComponent-subSubComponent { ... }
```

- double hyphen ``` -- ``` for modifier

```SCSS
.ComponentName--featured { ... }
```

- generic classes for states

```SCSS
.ComponentName { 
	&.active { ... } 
}
```

- no ``` # ``` IDs

```PHP
#WRONG# 
.header-nav { ... }

.left-button { ... }

.footer-links { ... }
```

```SCSS
// CORRECT
.primaryNav { ... }

.actionButton { ... }

.secondaryLinks { ... }
```

## Nesting order


```SCSS
.selector {
  // styles

  /* pseudo elements */
  &:after,
  &:before { ... }

  /* block modifiers & states */
  &--modifier { ... }

  &:hover,
  &.active { ... }

  &:first-child { ... }

  /* responsive */
  @include media(xxl) {
    // styles
  }

  /* children */
  > h1 { ... }
}
```

## Properties order 

Properties will be grouped by importance and scope. The following categories will be used:
- Positioning & relativity
- Box Model
- Visual display 
- Text 
- Behaviour

```SCSS
.selector {
	/* Positioning & relativity  */
	position: absolute;
	z-index: 10;
	top: 0;
	right: 0;

	float: left;
	clear: both;

	/* Box Model */
	display: none;

	width: 100%;
	min-width: 100px;
	max-width: 200px;

	height: 100%;
	min-height: 100px;
	max-height: 200px;

	padding: 10px;
		/* TRBL order for single sides 
		padding-top
		padding-right
		padding-bottom
		padding-left
		*/
	margin: 10px;
	
	/* Visual display */
	visibility: hidden;
	opacity: 0;
	overflow: hidden;

	background: url(‘../img/background.jpg’) no-repeat center center #FFF;
		/*
		background-color
		background-image
		background-position
		background-repeat
		*/
	border: 10px solid #333;
		/* TRBL order for single sides */
	border-radius: 5px;
	box-shadow: 0px 0px 5px rgba(0,0,0,0.5);

	list-style-type: disc;  (ul, ol)
	list-style-image: url(‘../bullet.png’);  (ul, ol)
	border-collapse: collapse;  (table)

	/* Text */
	font-family: sans-serif;
	font-size: 16px;
	font-weight: 700;
	font-style: italic;
	line-height: 1.4;
	
	color: #0F0;
	text-align: right;
	text-decoration: underline;
	text-transform: capitalize;
	word-wrap: break-word;

	letter-spacing: 2px;
	word-spacing: 5px;
	text-shadow: 2px 2px 2px rgb(12,12,12);

	transform: scale(1.2);

	/* Behaviour */
	cursor: pointer;

	transition: all 1s ease-in;
		/* 
		- name
		- duration
		- delay
		- easing
		*/
	animation: doMagic 1s ease-in-out infinite;
		/* 
		- name 
		- duration
		- delay
		- easing
		- iteration count
		- direction 
		*/
}
```
