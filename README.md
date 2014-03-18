Flint
=====

**Flint is a seemingly simple Sass based grid-system** 
capable of complex responsive layouts customized at each 
breakpoint, all while using a single mixin. All of your
layout settings are housed in a simple config file.

Flint handles the layout, you do the rest.

Config
------

Flint's config map is unique in the ability that you may
define an unlimited number of breakpoints for your
project. Whether that be 2 breakpoints, or even 12. 
You're in control.

Settings may be entered in `px` or `em`, and **flint**
will do the rest.

*Keep in mind, whatever unit you choose to use here needs to 
be used consistently throughout. No mixing `px` and `em`.*

```scss
$flint: (

	// grid configuration

	"config": (

		// define breakpoints

		"desktop": (
			"columns": 16,
			"breakpoint": 1280px,
		),
		"laptop": (
			"columns": 12,
			"breakpoint": 960px,
		),
		"tablet": (
			"columns": 8,
			"breakpoint": 640px,
		),
		"mobile": (
			"columns": 4,
			"breakpoint": 320px,
		),

		// additional grid settings

		"settings": (
			"default": "desktop",
			"grid": "fluid",
			"gutter": 10px,
			"max-width": false,
			"float-style": "left",
			"border-box-sizing": true,
			"debug-mode": true,
		),
	),
);
```

Foundation
----------

If you selected `border-box-sizing: true`, then it is 
*advised* to create a global foundation instance like so,

```scss
* {
	@include flint(foundation);
}
```

That way your output won't be riddled with `box-sizing`
declarations everytime you define a span.

Recursive shorthand
-------------------

```scss
.recursive {
	@include flint(3);
}
```

Outputs,
```scss
recursive {
	display: block;
	float: left;
	width: 17.1875%;
	margin: 0 0.78125%;
}
@media only screen and (min-width: 641px) and (max-width: 960px) {
	.recursive {
		width: 22.9166666667%;
		margin: 0 1.0416666667%;
	}
}
@media only screen and (min-width: 321px) and (max-width: 640px) {
	.recursive {
		width: 34.375%;
		margin: 0 1.5625%;
	}
}
@media only screen and (min-width: 0) and (max-width: 320px) {
	.recursive {
		width: 68.75%;
		margin: 0 3.125%;
	}
}
```

As you can see, since `desktop` is the framework `default`, it uses
the output for desktop as the base styles. You can set this to any
breakpoint you like. So if you like mobile-first, you can do that.

Recursive shorthand with identical context
------------------------------------------

Use this if your nested context is *identical* across all breakpoints.

```scss
//  .parent {
//  	   @include flint(6);
//  }

.recursive {
	@include flint(3, 6);
}
```

Outputs,
```scss
.recursive {
	display: block;
	float: left;
	width: 45.8333333333%;
	margin: 0 2.0833333333%;
}
@media only screen and (min-width: 641px) and (max-width: 960px) {
	.recursive {
		width: 45.8333333333%;
		margin: 0 2.0833333333%;
	}
}
@media only screen and (min-width: 321px) and (max-width: 640px) {
	.recursive {
		width: 45.8333333333%;
		margin: 0 2.0833333333%;
	}
}
@media only screen and (min-width: 0) and (max-width: 320px) {
	.recursive {
		width: 45.8333333333%;
		margin: 0 2.0833333333%;
	}
}
```

Recursive shorthand with variable context
-----------------------------------------

Use this if your context is *not* indentical across breakpoints.

```scss
//  .parent {
//	   @include flint(10 8 6 4);
//  }

.recursive {
	@include flint(2, 10 8 6 4);
}
```

Outputs,
```scss
recursive {
	display: block;
	float: left;
	width: 17.5%;
	margin: 0 1.25%;
}
@media only screen and (min-width: 641px) and (max-width: 960px) {
	.recursive {
		width: 21.875%;
		margin: 0 1.5625%;
	}
}
@media only screen and (min-width: 321px) and (max-width: 640px) {
	.recursive {
		width: 29.1666666667%;
		margin: 0 2.0833333333%;
	}
}
@media only screen and (min-width: 0) and (max-width: 320px) {
	.recursive {
		width: 43.75%;
		margin: 0 3.125%;
	}
}
```

Variable shorthand
------------------

Use this if your content needs different spans across each breakpoints.

```scss
.variable {
	@include flint(8 6 4 4);
}
```

Outputs,
```scss
.variable {
	display: block;
	float: left;
	width: 48.4375%;
	margin: 0 0.78125%;
}
@media only screen and (min-width: 641px) and (max-width: 960px) {
	.variable {
		width: 47.91667%;
		margin: 0 1.04167%;
	}
}
@media only screen and (min-width: 321px) and (max-width: 640px) {
	.variable {
		width: 46.875%;
		margin: 0 1.5625%;
	}
}
@media only screen and (min-width: 0) and (max-width: 320px) {
	.variable {
		width: 93.75%;
		margin: 0 3.125%;
	}
}
```

Variable shorthand with context
-------------------------------

Use this if you're nesting columns using the variable shorthand.

```scss
//  .parent {
//	   @include flint(16 12 8 4);
//  }

.variable {
	@include flint(14 10 6 2, 16 12 8 4);
}
```

Outputs,
```scss
recursive {
	display: block;
	float: left;
	width: 85.9375%;
	margin: 0 0.78125%;
}
@media only screen and (min-width: 641px) and (max-width: 960px) {
	.recursive {
		width: 81.25%;
		margin: 0 1.0416666667%;
	}
}
@media only screen and (min-width: 321px) and (max-width: 640px) {
	.recursive {
		width: 71.875%;
		margin: 0 1.5625%;
	}
}
@media only screen and (min-width: 0) and (max-width: 320px) {
	.recursive {
		width: 43.75%;
		margin: 0 3.125%;
	}
}
```

Wrapping in media queries
-------------------------

Use these if you need to apply breakpoint specific styling.

```scss
.wrap {
	@include flint(desktop) {
		// only desktop
	}
}
.wrap {
	@include flint(greater than mobile) {
		// all sizes above mobile
	}
}
.wrap {
	@include flint(10em greater than mobile) {
		// all sizes 10em above mobile
	}
}
.wrap {
	@include flint(less than tablet) {
		// all sizes under tablet
	}
}
.wrap {
	@include flint(1em less than laptop) {
		// all sizes 1em under laptop
	}
}
.wrap {
	@include flint(for desktop tablet) {
		// only for desktop and tablet
	}
}
.wrap {
	@include flint(from mobile to laptop) {
		// all sizes from mobile to laptop
	}
}
.wrap {
	@include flint(from desktop to infinity) {
		// all sizes from desktop to infinity
	}
}
```

Call by name
------------

Use if you want to define each span without shorthands.

```scss
.name {
	@include flint(desktop, 4);
}
```

Outputs,
```scss
.recursive {
	display: block;
	float: left;
	width: 23.4375%;
	margin: 0 0.78125%;
}
```

Gutter modifiers
----------------

Here are different gutter modifiers that may be called in when
defining spans. You should note, that when using shorthands
the gutter modifiers are recursive across all breakpoints.

```scss
// no left margin
.name {
	@include flint(desktop, 4, $gutter: alpha);
}

// no left right
.name {
	@include flint(desktop, 4, $gutter: omega);
}

// no margins
.name {
	@include flint(desktop, 4, $gutter: row);
}
```

Shift
-----

Much like the gutter modifiers, you may also call in a shift
parameter. This will cause the object to shift the desired amount
of columns using positive/negative left margins. 

```scss
// shift 4 columns to the right across all breakpoints
.name {
	@include flint(12 12 8 4, $shift: 4);
}

// shift 2 columns to the left across specified breakpoints
.name {
	@include flint(12 12 8 4, $shift: -2 -2 0 0);
}
```

One more cool thing about flint is that you are not bound to
the grid you define. Feel free to use decimals in your arguments
for extra fine tuned control over your layouts.

```scss
.so-much-control {
	@include flint(16, 12.1, 8, 4, $shift: 1.2, 0, 2, 0, $gutter: row);
}
```

**More features coming soon!**






