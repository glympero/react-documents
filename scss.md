## SCSS

BEM
Block - Element - Modifier
- modifier for button class ->
.button {

}
.button--link {

}
- usage : <button className="button button--link"></button>
- element for header:
.header {

}
.header__title {

}
.header__subtitle {

}

Structure:

/styles
  /base
    `_base.scss` //files that are imported are called partials and named with underscore first
  /components
    `_header.scss`
  styles.scss



In styles.scss we import base scss file with:

- @import './base/base' // we ommit underscore and file extension

### Scaling

Computing the value of 1rem; -> ie 16px

If we want to convert that to the base of 10: (ie 10px)

We set the html to scale down the 1rem to 10px by setting

html {
  font-size: 62.5%; //means multiply 16*62.5% = 10px = 1rem;
}

Then if we set
h1 {
  font-size: 2.2rem; //means that we are setting to 22px;
}
### margin
space between current selector and the things below it

### normalise css
Make sure that all browsers start from the exact same place
Reset css for more concise loading

- install yarn add normalize.css
- import to app.js above styles file
- add support for css & scss files by making the first s optional with a question mark
{
  test:/\.s?css$/,
  use: [
      'style-loader',
      'css-loader',
      'sass-loader'
  ]
}

## theming with variables
- use a *_settings.scss* file in order to store common things like colors, rem values etc
- import file first before other scss files in order for the other files to have access
  to variables

### center all of the content on the screen
- create a new file *_container.scss*
### css Functions
darken(colorToDarken, percentage);
darken(red, 10%);

### pseudo-class
: means pseudo class
.button:disabled {

}
