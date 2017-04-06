# SASS mixin flex grid
A sass mixin based on [fukol-grids](https://github.com/Heydon/fukol-grids).

Works with over 4 cols, but **4** is already a good number: do we need other cols in a web layout?

Take a look on a **[DEMO](http://codepen.io/timhecker/details/RpmRzm/)**


## SASS

```sass

// mixin to calculate item width
@mixin item-width($width) {
	max-width: $width; // for IE
	flex-basis: $width; // for iOS
}

// mixin for flex grid
@mixin flex-grid($item-name, $cols: 2, $gap: 0) {
	
  // grid works only from small viewport and beyond
  @media screen and (min-width: 48em) {
    display: flex;
    flex-wrap: wrap;

    @if $gap > 0 {
      overflow: hidden;
      margin-left: -($gap);
      margin-right: -($gap);
    }
  }

  .#{$item-name} {
    width: 100%; // for IE 10
		
		@if $gap > 0 {
			margin-bottom: $gap * 2; // vertical space between items, relative to horizontal space
		}

    // small viewport
    @media screen and (min-width: 48em) {
      // contextual var
			$item-width: if($gap > 0, calc(50% - #{$gap * 2}), 50%);
      // ---------------
			@include item-width($item-width);
      flex-grow: 1;
      flex-shrink: 0;
      
      @if $gap > 0 {
        margin-left: $gap;
        margin-right: $gap;
       }
    }

    // MORE THAN 2 COLS
    @if $cols >= 3 {
      // large viewport
      @media screen and (min-width: 80em) {
        // contextual var
				$item-width: if($gap > 0, calc((100% / #{$cols}) - #{$gap * 2}), (100% / $cols));
        // ---------------
     		@include item-width($item-width);
      }
    }

    // MORE THAN 3 COLS
    @if $cols >= 4 {
      // large viewport
      @media screen and (min-width: 80em) {
        // contextual var
				$item-width: if($gap > 0, calc((100% / 3) - #{$gap * 2}), (100% / 3)); // always 3 cols on large viewport
        // ---------------
        @include item-width($item-width);
      }
      
      // extra-large viewport
      @media screen and (min-width: 100em) {
        // contextual var
				$item-width: if($gap > 0, calc((100% / #{$cols}) - #{$gap * 2}), (100% / $cols));
        // ---------------
        @include item-width($item-width);
      }
    }

    // MORE THAN 4 COLS
    @if $cols >= 5 {
      // large viewport
      @media screen and (min-width: 80em) {
        // contextual var
				$item-width: if($gap > 0, calc((100% / 4) - #{$gap * 2}), (100% / 4)); // always 4 cols on large viewport
        // ---------------
        @include item-width($item-width);
      }
      
      // extra-large viewport
      @media screen and (min-width: 100em) {
        // contextual var
				$item-width: if($gap > 0, calc((100% / #{$cols}) - #{$gap * 2}), (100% / $cols));
        // ---------------
        @include item-width($item-width);
      }
    }
  }
}
```

### Usage

**without** space between columns:

```sass
.my-grid {
  @include flex-grid(my-grid__item, 3);
}
```


**with** space between columns:

```sass
.my-grid {
  @include flex-grid(my-grid__item, 3, 2vh);
}
```
