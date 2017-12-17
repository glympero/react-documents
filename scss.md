## SCSS

Structure:

/styles
  /base
    `_base.scss` //files that are imported are called partials and named with underscore first
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
