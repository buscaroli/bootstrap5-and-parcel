# LEARNING BOOTSTRAP-5 AND PARCEL

I have decided to learn how to modify Bootstrap's classes in order to be able to better customise a page build with the CSS framework.

In order to do that Bootstrap had to be installed with npm and there is the need of a build tool, in this case Parcel.

## Tools

- npm
- node
- parcel
- bootstrap
- bootstrap-icons

## Learning points

### Parcel

Parcel was straight-forward to use as a builer, make sure you have installed it globally with

```
npm install -g parcel-bundler
```

and then just follow the instructions on [Bootstrap's web page](https://getbootstrap.com/docs/5.0/getting-started/parcel/).

The main steps are:

- npm i bootstrap bootstrap-icons
- create Parcel's recommended folder structure:

```
project-name/
|
├── build/
|
├── scss/
│   └── custom.scss
└── src/
    └── index.html
    └── index.js
```

- import bootstrap inside src/index.js

```
  import * as bootstrap from 'bootstrap';
```

- insert a script tag inside index.html, just before the end of the body

```html
<body>
  <!-- all your HTML here-->
  <script src="./index.js"></script>
</body>
```

- prepare src/scss/custom.scss in order to be able to modify Bootstrap's classes.
  NB Variables you want to override need to be stated BEFORE importing Bootstrap's ones as the framework needs to know what variable you are trying to override!!

```scss
// 1) Define the defauls variable overrides here (THIS GOES BEFORE!)

$primary: rgb(199, 203, 245);
$warning: rgb(247, 231, 54);

// 2) Now import Bootstrap's classes (THIS GOES AFTER!)
@import '../node_modules/bootstrap/scss/bootstrap';

// 3) You can add your owncustom classes here, eg:

.customCard {
  min-width: 300px;
  max-width: 400px;
}
```

- add the link to your scss file inside the <head> ofindex.html:

```html
<head>
  <link rel="stylesheet" href="../scss/custom.scss" />
</head>
```

- add Parcel's own scripts into your package.json file:

```json

"scripts": {
    "dev": "parcel ./src/index.html",
    "prebuild": "npx rimraf build",
    "build": "parcel build --public-url ./ ./src/index.html --experimental-scope-hoisting --out-dir build"
  }

```

- Parcel's script will reload your page every time you save your files, just run it with:

```bash
  npm run dev
```

### Bootstrap

I have tried to use Bootstrap's row and column system to create three card that would respond to the screen's width.
**However** I have found out that the cards were not centered and a big margin was left on the right side of the screen, which was particularly evident once the cards switched to a single column layout.

I have very kindly been provided with a solution by two of my fellow trainee engineers at Futureproof ( [William](https://github.com/Izgardon) and [Tom](https://github.com/tomhughes87) ) which consisted of creating a custom class and implement a CSS grid.

That solution worked very well but with trial and fail I have found a different one, which consist in adding a margin property of " 0 auto " to the card, via a custom class (in this case called customCard):

```scss
// scss/custom.scss

.customCard {
  min-width: 300px;
  max-width: 400px;
  margin: 0 auto; // centering the card
  background-color: rgb(74, 70, 70);
  letter-spacing: 2px;
}
```

```html
<-- src/index.html -->

<div class="container-fluid mt-2">
  <div class="row">
    <!-- card 1 -->
    <div class="col">
      <div class="card customCard">
        <!-- .customCard -->
        <img
          src="../assets/natalya-zaritskaya-unsplash.jpeg"
          class="card-img-top"
          alt="..."
        />
        <div class="card-body">
          <h5 class="card-title text-center display-5">Family</h5>
          <p class="card-text ">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolore quos
            inventore facilis ad alias, odio, eaque recusandae incidunt natus
            repudiandae doloribus sint non nostrum.
          </p>
          <a href="#" class="btn btn-primary w-100 py-3 bg-warning"
            ><span class="lead">Checkout</span></a
          >
        </div>
      </div>
    </div>

    <div>Card 2 in here</div>

    <div>Card 3 in here</div>
  </div>
</div>
```
