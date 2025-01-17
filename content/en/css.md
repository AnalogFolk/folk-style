---
title: CSS
description: Structure and syntax for working on CSS and Sass style sheets at AnalogFolk
position: 3
category: CSS, front-end
---

## CSS

The ruleset [defined by Airbnb][airbnb-css] for their CSS is the best one-stop
set of rules and should be followed in projects for Analogfolk.

Consider the implementation of prettier, and/or stylelint in your project as a
way to enforce a consistent style.

### Formatting & Syntax

- Use **two spaces** for indentation
- Use a space to separate the colon after the property from its value
- Always end a `property: value` pair with a semicolon and new line
- Use one discreet selector per line in multi-selector rule sets.

```css
.box--selected,
.item--selected,
.title--selected {
}
```

- Include a single space before the opening brace of a rule set.
- Use one level of indentation for each declaration
- Use lowercase hex values
- use long form hex values (seven characters including the hash character) for consistency
- Use single quotes consistently
- Include a space after each comma in comma-separated property or function values
- Separate each rule set with a blank line

See [this codepen][codepen1] for examples of correct usage.

#### Declaration ordering

If declarations are to be consistently ordered, it SHOULD be in
accordance with a single, simple principle. Define either
[clustered ordering][css-clustered] or [alphabetical ordering][css-alpha],
depending on the requirements and preferences of the team. The standard
approach MUST be documented. Code reviews should enforce the standard.

**Use caution** - retrospectively ordering properties alphabetically after
a lot of css has been written can be a cause of style regression bugs.

### Pre-processing

We use SASS (with SCSS syntax) as a preprocessor of choice.

- Use `.scss` syntax not `.sass`
- Do not nest selectors more than three levels deep
- Avoid using `@extend` if possible (use mixins instead), but if you do use it...
  - Always place `@extend` statements on the first line of a declaration
  - only extend `%placeholder` classes
- Where possible, group `@include` statements at the top of a
  declaration block, after any `@extend` statements

```scss
.block {
  @extend %base-block;

  &__element {
    property: value;
  }

  &--modifier {
    property: value;
  }
}
```

### Units and Colours

- Omit units after "0"
- Omit leading "0"s in values (i.e. `.5em` not `0.5em`)

### Specificity

Generally use of BEM and OO principles should avoid falling into any of the
bad practice below.

- Use the least number of selectors required to style an element. **Don't
  nest SCSS or CSS selectors more than three levels deep**
- Ideally use [BEM][bem-101] and don't nest or stack selectors
- Avoid adding element selectors to class definitions
- Avoid using Ids in style definitions
- Avoid using `!important` [except in case of SMACSS state][smacss-state] rules

```scss
// BAD
section.intro {
  font-family: 'Open Sans', sans-serif;
  border: 0px;
}

.header {
  .title {
    .primary {
      em {
        font-weight: bold;
        line-height: 0.5rem;
      }
    }
  }
}

#nav {
  display: inline;
}
```

### Class naming

- You SHOULD use kebab case. i.e., hyphens not underscores or camelCase for
  class names
- Underscores are acceptable if you're using BEM syntax
- `camelCase` is acceptable if a classname is tied to a reactive component
  name (see [the Airbnb OOCSS/BEM advice][airbnb-oocss] for reference)

```scss
// BAD
.valid-class-name {
}

.invalidClassName,
.invalid_classname {
}

// acceptable
.infoBlock {
  &__element {
    background: yellow;
  }

  &--modifier {
    color: red;
  }
}
```

- If an element is to have functionality bound to it in Javascript, use a
  className prepended with 'js-' to identify it. Avoid binding to the same
  class in both CSS and Javascript.

### Media Queries

- Add media query blocks for an element at the end of the declaration
  block for that element

### Modularisation

Use [SMACSS][smacss] principles for modular CSS. Establish top level
folders with the following categories :

- **[Base][smacss-base]**
  Project-wide variables; colours, breakpoints, font imports, file locations
- **[Layout][smacss-layout]**
  Overall layout rules; outer grid dimensions, grid etc.
- **[Module][smacss-module]**
  Functional modules within site, separated into individual files
- **[State][smacss-state]**
  Modifications based on interaction - i.e. hidden and visible states
- **[Theme][smacss-theme]**
  Customisations based on overall site context

Ideally include a main.scss file at the top of the folder structure.
Import an index files from each of the subsidiary folders, and import
files in each directory by using `@import` rules in that index.scss

```text
./app
  ˪/styles
    ˫/base
    | ˫index.scss
    | ˪_colours.scss
    ˪main.scss
```

### Further reading, and acknowledgements

- [Idiomatic CSS][idiomatic] by Nicolas Gallagher
- [Don't use @extend][dont-extend] by Tiffany B. Brown

[airbnb-css]: https://github.com/airbnb/css
[css-clustered]: https://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685
[css-alpha]: https://meiert.com/en/blog/on-declaration-sorting/
[codepen1]: http://codepen.io/gwawr/pen/VaROdB
[bem-101]: https://css-tricks.com/bem-101/
[airbnb-oocss]: https://github.com/airbnb/css#oocss-and-bem
[smacss]: https://smacss.com/book/categorizing
[smacss-base]: http://smacss.com/book/type-base
[smacss-layout]: http://smacss.com/book/type-layout
[smacss-module]: http://smacss.com/book/type-module
[smacss-state]: http://smacss.com/book/type-state
[smacss-theme]: http://smacss.com/book/type-theme
[idiomatic]: https://github.com/necolas/idiomatic-css
[dont-extend]: https://webinista.com/updates/dont-use-extend-sass/
