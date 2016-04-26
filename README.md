# Bidi SASS improvements

Redefines the compact variant mixins from `bi-app-sass` library to make writing direction aware
styles more _natural_. In addition the improvements include some extensions not defined by
`bi-app-sass`.

## Overrides
While you have to use comma-separated parameter list for all sides like this
```scss
.foo {
    @include padding(1px, 2px, 3px, 4px);
}
```
the overrides redefine that to allow single parameter
```scss
.foo {
    @include padding(1px 2px 3px 4px);
}
```
which can be used also for other variants of the compact style syntax
```scss
.foo {
    @include padding(1px);
    @include padding(1px 2px);
    @include padding(1px 2px 3px);
    @include padding(1px 2px 3px 4px);
}
```
where the first three variants result in usual direction unrelated CSS and the last one is converted
into a direction aware style declaration. The result of the one above would be in `ltr` case:
```css
.foo {
    padding: 1px;
    padding: 1px 2px;
    padding: 1px 2px 3px;
    padding: 1px 2px 3px 4px;
}
```
and in `rtl` case
```css
.foo {
    padding: 1px;
    padding: 1px 2px;
    padding: 1px 2px 3px;
    padding: 1px 4px 3px 2px; /* right and left are swapped */
}
```

## Extensions
The library also adds mixins to swap `::before` and `::after` selectors
```scss
.foo {
    @include before((
        padding: 1px 2px 3px 4px,
        margin: .2em .4em .6em .8em
    ));
}
```
which is converted for `ltr` to
```css
.foo:before {
    padding: 1px 2px 3px 4px;
    margin: .2em .4em .6em .8em;
}
```
and for `rtl` to
```css
.foo:after {
    padding: 1px 2px 3px 4px;
    margin: .2em .4em .6em .8em;
}
```