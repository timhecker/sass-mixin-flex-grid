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
    flex-grow: 1;
    flex-shrink: 0;

    @if $cols >= 4 {
      @media screen and (min-width: 48em) {
        $my-cols: $cols - 2;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        max-width: $item-width; // for IE
        flex-basis: $item-width; // for iOS
        margin-left: $gap;
        margin-right: $gap;
      }
    } @else if $cols = 3 {
        @media screen and (min-width: 48em) {
          $my-cols: 2;
          $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
          max-width: $item-width;
          flex-basis: $item-width;
          margin-left: $gap;
          margin-right: $gap;
        }
    } @else {
        @media screen and (min-width: 48em) {
          $item-width: calc((100% / #{$cols}) - #{$gap * 2});
          max-width: $item-width;
          flex-basis: $item-width;
          margin-left: $gap;
          margin-right: $gap;
        }
    }


    @if $cols >= 4 {
      @media screen and (min-width: 60em) {
        $my-cols: $cols - 1;
        $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
        flex-basis: $item-width;
        max-width: $item-width;
      }
    } @else {
        @media screen and (min-width: 60em) {
          $my-cols: $cols;
          $item-width: calc((100% / #{$my-cols}) - #{$gap * 2});
          flex-basis: $item-width;
          max-width: $item-width;
        }
    }

    @if $cols >= 4 {
      @media screen and (min-width: 80em) {
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
