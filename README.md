# Mediatic

## Very Simple and Advanced Media Query Mixin for Sass

### Install

```bash
npm install --save mediatic

// or with Yarn

yarn add mediatic
```

### Usage

```scss
// Input
@include mediatic(sm md portrait dark) {
    /* styles */
}

// Output
@media all and (min-width: 576px) and (max-width : 767px) and (orientation : portrait) and (prefers-color-scheme: dark) {
    /* styles */
}
```

### Variations

```scss
// Input
@include mediatic(/* values goes here */) { /* styles */ }

// ALL OPINIONS
// Devices  :   all (default), screen, speech, print
// Keywords :   xs, sm, md, lg, xl
//              portrait, landscape
//              dark, light
//              retina
// Numbers :    Any positive number with/without any unit
//              400 or 400px, 30rem
```

### Retina

```scss
// Input
@include mediatic(retina) { /* styles */ }

// Output
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), only screen and (min-device-pixel-ratio: 1.3), only screen and (min-resolution: 1.3dppx), only screen and (min-resolution: 2dppx) {
    /* styles */
}
```

### Numeric Values

```scss
// Input
@include mediatic(320px) { /* styles */ }
@include mediatic(320px, 768px) {}
// or
@include mediatic(320) { /* styles */ }
@include mediatic(320, 768) { /* styles */ }

// Output
@media only screen and (min-width : 320px) { /* styles */ }
@media only screen and (min-width : 320px) and (max-width: 768px) { /* styles */ }
```

**Note :** You can use any CSS unit instead of px. Even you can set it defaultly. To learn how to do it, follow the [configuration](###Configuration) section.

```scss
// Input
@include mediatic(20rem, 40rem) { /* styles */ }

// Output
@media only screen and (min-width: 20rem) and (max-width: 40rem) { /* styles */ }
```

### Device types

```scss
// input.scss
@include mediatic(print) {
    /* styles */
}

// output.css
@media only print {
    /* styles */
}
```

### Configuration

Go into _config.scss file and there replace below values with yours.

#### To change breakpoints

```scss
$breakpoints : (
    sm : 576px,
    md : 768px,
    lg : 992px,
    xl : 1200px
) !default;
```

##### To Change Default Device

```scss
$default-device : all !default;
```

#### To change default unit for unitless numbers

```scss
$default-unit-for-unitless: 'px' !default;
```

##### To Add New Keywords

```scss
$queries : (
    ..............,
    ..............,
    ..............,
    my-custom-query : (
        min-width: 768px,
        max-width: 1024px,
        orientation: portrait,
        prefers-color-scheme: dark
    )
);

// Now use it
@include mediatic( my-custom-query ) { /* styles */ }

// Output
@media only screen and (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) and (prefers-color-scheme: dark) { /* styles */ }
```
