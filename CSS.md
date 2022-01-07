# CSS Style Guide
## Whitespace and indentation
 * Use tabs instead of spaces to indent properties.
 * One selector per line.
 * One declaration per line.
 * The opening brace of a CSS block must go on the same line as the selector.
 * Include a single space after a colon (but not before).
 * Include a semicolon at the end of every declaration, including the last one.

## Naming convention
Classes and IDs must be lowercase, with hyphens to separate words and terms.
```css
/* bad */
.dialogcontainer {
}

/* good */
.dialog-container {
}
```
## Selectors
Avoid referencing the HTML tag in the selector. Use as little specificity as possible.

## Properties
### Order
Properties are ordered by their type, then alphabetically (roughly). These groups are:
 * Positioning, DOM, transforms
 * Background and box-shadow
 * Text
 * Animations and transitions

### Shorthand
Use shorthand properties where possible. These let you condense multiple properties into one.
Examples include:
 * `background`
 * `border`
 *  `border-radius`
 * `inset`

There are a few exceptions where certain shorthand properties make CSS code harder to read. 
These properties are:
 * `flex`
 * `font`
 * `font-variation-settings`
 * `grid`

```css
/* bad */
.foo {
	padding-top: 1rem;
	padding-bottom: 1rem;
	padding-left: 1rem;
	padding-right: 1rem;
}

/* good */
.foo {
	padding: 1rem;
}
```
### Vendor prefixes
Browsers are currently working towards deprecating vendor prefixes, and instead put experimental CSS features behind a feature flag.
Unfortunately, some properties can't be avoided for compatibility reasons. Use vendor prefixes when you need to support older browsers.

Vendor prefixes must go before the main prefix so that they render correctly.
```css
.foo {
	-webkit-user-select: none;
	user-select: none;
}
```
To find compatibility data for a property, refer to [*MDN Web Docs*](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) and [*Can I Use*](https://caniuse.com/).

The vendor prefixes that exist are:
 * `-webkit-`: Chrome, Safari, iOS, post-webkit versions of Opera
 * `-o`: Pre-webkit versions of Opera (no longer needed; don't use this prefix!)
 * `-moz-`: Firefox
 * `-ms-`: IE, Microsoft Edge

### Z-index
Z-index layers controls the z-coordinate of HTML elements and override the order in which they are rendered, which is known as the "stacking context".[^w3-stacking-context]
However, avoid using the `z-index` property if possible. Use the natural order of the DOM.

If this can't be avoided, the `z-index` of the component should be stored inside a CSS variable.
All z-index variables should appear in the same stylesheet, in order from least to greatest, e.g:
```css
:root {
	--z-index-dialog: 100;
	--z-index-modal: 200;
}
```

Example components that can and **need** a z-index include overlay-like elements such as popups, dialogs, and tooltips.

## Keywords and values
### !important keyword
Avoid using this keyword; you won't need it.
The `!important` keyword overrides the style for a selector with a higher specificity.
While it *can* work as a hot-glue-like hack, it makes CSS code less maintainable in the long run.

To override a rule, use the same selector as the original rule containing those styles.

### Colors
 * Use shorthand values where possible. E.g `#fff` instead of `#ffffff`
 * Use color values instead of named keywords. E.g `#fff` instead of `white`. The only exception is the `transparent` keyword. 
 * As of CSS Color Module Level 4[^w3-css-color-4]:
   * the hexadecimal notation now supports alpha transparency via `#rrggbbaa` notation (with `#rgba` as shorthand notation) [in newer browsers](https://caniuse.com/mdn-css_types_color_alpha_hexadecimal_notation)
   * the `rgb()` function now supports alpha transparency in [newer browsers](https://caniuse.com/mdn-css_types_color_rgb_function_accepts_alpha). Prefer `rgb()` over `rgba()`.

Please keep in mind that the contrast between background and foreground colors are accessible. Use the WCAG 2.0 guidelines to determine if your design meets the minimum requirements. At a minimum it should meet AA, and ideally AAA if possible.

> Unfortunately, the `color-contrast()` function [is still experimental](https://caniuse.com/mdn-css_types_color_color-contrast) and not supported by any browsers.
>
> This feature is defined in the *CSS Color Module Level 5* specification.[^w3-css-color-5]

### Numeric units
For responsive design, use `rem` units instead of `px` and `em` (generally).
 * The `px` unit is not the same value across different devices, since devices have different pixel densities.
 * The `em` unit is relative to the parent element. This makes values harder to calculate and keep track of as the DOM becomes more complex.
 * The `rem` unit is relative to the *root* element.

Use numeric values on a scale if possible for consistency, such as 1/4 or 1/8:
* 1/4: 0, .25, .75, 1
* 1/8: 0, .125, .375, .625, .875, 1 (also includes 1/4 values)

If a numeric value is 0, omit the unit. Omit leading zeroes.

```css
/* bad */
padding: 0.5rem 0rem;

/** good */
padding: .5rem 0;
```

## Best Practices
### Avoid using absolute positioning
Avoid using absolute positioning; `position: absolute;`. This takes the element out of the normal DOM flow, and creates a new *stacking context*.[^w3-stacking-context][^w3-pos-absolute]
This declaration usually goes in hand with box inset properties (`top`/`right`/`bottom`/`left`) to set its location on the page. This often requires magic numbers, or complex `calc()` expression calls, making it hard to maintain.

> tl;dr Use absolute positioning as a **last resort**, if nothing else works.

[^w3-stacking-context]: CSS Working Group, ed. (15 November 2021). ["CSS 2 § 9.9 Layered representation"](https://drafts.csswg.org/css2/#stacking-context). Retrieved 6 January 2022.
[^w3-pos-absolute]: CSS Working Group, ed. (16 December 2021). ["CSS Positioned Layout Module Level 3 § 2. Choosing A Positioning Scheme: position property"](https://www.w3.org/TR/css-position-3/#valdef-position-absolute). Retrieved 6 January 2022.
[^w3-css-color-4]: CSS Working Group, ed. (15 December 2021). ["CSS Color Module Level 4 § 5. sRGB Colors"](https://www.w3.org/TR/css-color-4/#numeric-srgb). Retrieved 6 January 2022.
[^w3-css-color-5]: CSS Working Group, ed. (15 December 2021). ["CSS Color Module Level 5 § 3. Selecting the most contrasting color: the color-contrast() function"](https://drafts.csswg.org/css-color-5/). Retrieved 6 January 2022.