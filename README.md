Sass (SCSS) mixin for easy media query breakpoint managing
===
The mixin I currently use for breakpoints. Breakpoints are defined in PXs, because it's easier to read for humans. But they are converted to EMs, because they provide more consistency between different browsers. ( See this study: http://zellwk.com/blog/media-query-units/)


how to use
---
Define your breakpoints in px
```SASS
$breakpoints: 480 640 800 960 1200 1480 1840 2080;
```

Copy the file into the folder where your main-scss-file is.
Include this file in your main-scss-file like this:
```SASS
@import 'breakpoints';
```

The function:
```SASS
@mixin brp($name) {
	@for $i from 1 through length($breakpoints) {
		$px_value: nth($breakpoints, $i);

		@if $name == 'b'+$i {
			@media all and (min-width: #{$px_value/16}em) {
				@content;
			}
		}
		@if $name == 'b'+$i+'max' {
			@media all and (max-width: #{$px_value/16 - 0.0635}em) {
				@content;
			}
		}
	}
}
```

Now you can do e.g.:
```SASS
body {
	@include brp(b2max) {
		background-color:green;
	}
	@include brp(b4) {
		background:red;
	}
}
```
...which translates to:
```SASS
@media all and (max-width: 39.937em) {
	body {
		background-color: green;
	}
}

@media all and (min-width: 60em) {
    body {
      background: red;
  	}
}
```
