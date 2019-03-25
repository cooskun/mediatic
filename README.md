# Mediatic

## Very Simple and Advanced Media Query Mixin for Sass

### Install

```bash
npm install --save mediatic

// or with Yarn

yarn add mediatic
```

### Summary

Media queries might be really painful sometimes, specially in large projects. You have to think about many different variations of code than only device size. Then, queries gonna be longer and longer. **Mediatic** is here to solve it for you. Everything you need stays between only two paranthesis. Specific keywords, numbers, even pure CSS queries. Also, specific keywords are extendable. I explained how under the [configuration](####configuration) title.

First, look at the next follow lines and see how **Mediatic** survives you against complex queries.

```scss
// Input
@include mediatic(min-xs, 767, orientation portrait, prefers-color-scheme: dark) {
    /* styles */
}

// Output
@media only screen and (min-width: 320px) and (max-width : 767px) and (orientation : portrait) and (prefers-color-scheme: dark) {
    /* styles */
}
```

Looks good? It could be even shorter as below.

```scss
@include mediatic(320, 767, portrait, dark) {
    /* styles */
}

// Output
@media only screen and (min-width: 320px) and (max-width : 767px) and (orientation : portrait) and (prefers-color-scheme: dark) {
    /* styles */
}
```

### Usage

```scss
// Input
@include mediatic(/* values goes here */) { /* styles */ }

// ALL OPINIONS
// Keywords :   xs, sm, md, lg, xl
//              min-xs, min-sm, min-md, min-lg, min-xl
//              max-xs, max-sm, max-md, max-lg
//              portrait, landscape
//              dark, light
//              retina
// Numbers :    Any positive number with/without any unit
//              400 or 400px, 30rem
// Pure CSS :   Any valid pure CSS query with/without parantesis
//              min-width : 768px, orientation : portrait
// Short CSS :  Any valid css query only with their properties and values
//              min-width 768px, orientation portrait
//              or all together => min-width 768px orientation portrait
```

### Examples

#### Min Device Size

```scss
// Input
@include mediatic(min-xs) { /* styles */ }
// or
@include mediatic(320px) { /* styles */ }
// or
@include mediatic(320) { /* styles */ }
// or
@include min(320) { /* styles */ }
// or with shortand
@include min-xs() { /* styles */ }

// Output
@media only screen and (min-width: 320px) { /* styles */ }

// ALL OPINIONS
// min-xs, min-xs(): 320px
// min-sm, min-sm(): 576px
// min-md, min-md(): 768px
// min-lg, min-lg(): 992px
// min-xl, min-xl(): 1200px
// min( $value )
```

#### Max Device Sizes

```scss
// Input
@include mediatic(max-xs) { /* styles */ }
// or
@include mediatic(575px) { /* styles */ }
// or
@include mediatic(575) { /* styles */ }
// or
@include max(575) { /* styles */ }
// or with shortand
@include max-xs() { /* styles */ }

// Output
@media only screen and (max-width: 575px) { /* styles */ }

// ALL OPINIONS
// max-xs, max-xs(): 575px
// max-sm, max-sm(): 767px
// max-md, max-md(): 991px
// max-lg, max-lg(): 1199px
// max( $value )
```

#### Between Device Sizes

```scss
// Input
@include mediatic(min-sm, max-md) { /* styles */ }
// or
@include mediatic(576px, 991px ) { /* styles */ }
// or
@include mediatic(576, 991) { /* styles */ }
// or
@include between(576, 991) { /* styles */ }

// Output
@media only screen and (min-width: 576px) and (max-width: 991px) { /* styles */ }
```

#### Certain Device Sizes

```scss
// Input
@include mediatic(md) { /* styles */ }
// or with shortand
@media md() { /* styles */ }

// Output
@media only screen and (min-width: 768px) and (max-width: 991px) { /* styles */ }

// ALL OPINIONS
// xs, xs(): 320px-575px
// sm, sm(): 576px-767px
// md, md(): 768px-991px
// lg, lg(): 992px-1199px
```

#### Vertically/Horizontaly Absolute Device Sizes

```scss
// Input
@include width(1024px) { /* styles */ }
@include height(768px) { /* styles */ }
// or
@include width(1024) { /* styles */ }
@include height(768) { /* styles */ }

// Output
@media only screen and (width: 1024px) { /* styles */ }
@media only screen and (height: 768px) { /* styles */ }
```

#### Orientation

```scss
// Input
@include mediatic(portrait) { /* styles */ }
// or
@include orientation(portrait) { /* styles */ }
// or with shortand
@include portrait() { /* styles */ }

// Output
@media only screen and (orientation: portrait) { /* styles */ }

// ALL OPINIONS
// mediatic(portrait / landscape)
// orientation(portrait / landscape)
// portrait(), landscape()
```

#### Retina

```scss
// Input
@include mediatic(retina) { /* styles */ }
// or
@include retina() { /* styles */ }

// Output
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), only screen and (min-device-pixel-ratio: 1.3), only screen and (min-resolution: 1.3dppx), only screen and (min-resolution: 2dppx) {
    /* styles */
}
```

#### Dark/Light Mode (MacOS Mojave)

```scss
// Input
@include mediatic(dark) { /* styles */ }
// or
@include color-scheme(dark) { /* styles */ }
// or
@include dark() { /* styles */ }

// Output
@media only screen and (prefers-color-scheme: dark) { /* styles */ }

// All opinions
// mediatic(dark / light)
// color-scheme(dark / light )
// dark(), light()
```

#### Pure CSS Query

```scss
// Input
@include mediatic(min-width:320px, max-width:768px, orientation:portrait) { /* styles */ }

// Output
@media all and (min-width: 320px) and (max-width: 768px) { /* styles */ }
```

#### Short CSS Queries

```scss
// Input
@include mediatic(min-width 320px max-width 768px orientation portrait) { /* styles */ }

// Output
@media only screen and (min-width: 320px) and (max-width: 768px) and (orientation: portrait) { /* styles */ }
```

#### Numeric Values

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

**Note :** You can use any CSS unit instead of px. Even you can set it defaultly. To learn how to do it, follow the [configuration](####Configuration) section.

```scss
// Input
@include mediatic(20rem, 40rem) { /* styles */ }

// Output
@media only screen and (min-width: 20rem) and (max-width: 40rem) { /* styles */ }
```

#### Configuration

Go into _config.scss file and there replace below values with yours.

##### To Change Breakpoints

```scss
$Breakpoints : (
    xs : 320px,
    sm : 576px,
    md : 768px,
    lg : 992px,
    xl : 1200px
) !default;
```

##### To Change Default Device

```scss
$default-device : 'only screen' !default;
```

#### To change default unit for unitless numbers

```scss
$default-unit-for-unitless: 'px' !default;
```

##### To Add New Keywords

```scss
$Queries : (
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

### Short Mixins

```scss
@include xs() {}                                            // Device is x-small
@include sm() {}                                            // Device is small
@include md() {}                                            // Device is medium
@include lg() {}                                            // Device is large
@include min-xs() {}                                        // Device is minimum x-small
@include min-sm() {}                                        // Device is minimum small
@include min-md() {}                                        // Device is minimum medium
@include min-lg() {}                                        // Device is minimum large
@include min-xl() {}                                        // Device is minimum x-large
@include max-xs() {}                                        // Device is maxumum x-small
@include max-sm() {}                                        // Device is maximum small
@include max-md() {}                                        // Device is maximum medium
@include max-lg() {}                                        // Device is maximum large
@include width( $value ) {}                                 // Device width is equal to value
@include height( $value ) {}                                // Device height is equal to value
@include min( $value ) {}                                   // Device is equal or bigger than $value
@include max( $value ) {}                                   // Device is equal or smaller than $value
@include between( $min, $max ) {}                           // Device is between $min and $max
@include orientation( $value: portrait/landscape ) {}       // Device orientation is $value
@include portrait() {}                                      // Device orientation is portrait
@include landscape() {}                                     // Device orientation is landscape
@include retina() {}                                        // Device has retina screen
@include color-scheme( $value: dark/light ) {}              // Device preferred color is $value (For Mojave color mode)
@include dark-mode() {}                                     // Device preffered color is dark
@include light-mode() {}                                    // Device preffered color is light
@include ratio ( $value ) {}                                // Device ratio is equal value
```