# SASS mixin flex grid
A sass mixin based on [fukol-grids](https://github.com/Heydon/fukol-grids).

Works with until 4 cols: do we need other cols in a web layout?


## SASS

```sass

@mixin flex-grid($cols, $gap, $item-name) {
  display: flex;
  flex-wrap: wrap;
  margin-left: (-$gap);
  margin-right: (-$gap);

  .#{$item-name} {
    width: 100%; // for IE 10
    flex-grow: 1;
    flex-shrink: 0;

    // small viewport
    @media screen and (min-width: 48em) {
      @if $cols >= 4 {
        $my-cols: $cols - 2;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        max-width: $item-width; // for IE
        flex-basis: $item-width; // for iOS
        margin-left: $gap;
        margin-right: $gap;
      }
      @else if $cols = 3 {
        $my-cols: 2;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        max-width: $item-width;
        flex-basis: $item-width;
        margin-left: $gap;
        margin-right: $gap;
      }
      @else {
        $item-width: calc((100% / #{$cols}) - #{$gap * 2});
        max-width: $item-width;
        flex-basis: $item-width;
        margin-left: $gap;
        margin-right: $gap;
      }
    }

    // medium viewport
    @media screen and (min-width: 60em) {
      @if $cols >= 4 {
        $my-cols: $cols - 1;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        flex-basis: $item-width;
        max-width: $item-width;
      }
      @else {
        $my-cols: $cols;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        flex-basis: $item-width;
        max-width: $item-width;
      }
    }

    // large viewport
    @media screen and (min-width: 80em) {
      @if $cols >= 4 {
        $my-cols: $cols;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        flex-basis: $item-width;
        max-width: $item-width;
      }
    }
  }
}
```

### Usage

```sass
.my-grid {
  @include flex-grid(3, 1vw, 'my-grid__item')
}
```
