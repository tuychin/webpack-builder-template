<div align="center">
  <h1>Webpack builder template</h1>
  <p>
    This Webpack template, link files for use in a browser,
    but it is also capable of converting, compressing and packaging resource.
  </p>
</div>

## Builder Setup:

``` bash
# Download repository:
git clone https://github.com/tuychin/webpack-builder-template

# Go to the app:
cd webpack-builder-template

# Install dependencies:
npm install

# Server with hot reload at http://localhost:8081/
npm run dev

# Output will be at build/ folder
npm run build
```

## Project Structure:

* `src/index.html` - main app HTML
* `src/scss` - put custom app SCSS styles here. Don't forget to import them in `index.js`
* `src/css` - the same as above but CSS here. Don't forget to import them in `index.js`
* `src/img` - put images here. Don't forget to use correct path: `assets/img/some.jpg`
* `src/js` - put custom app scripts here
* `src/index.js` - main app file where you include/import all required libs and init app
* `src/static/` - folder with extra static assets that will be copied into output folder

<div align="center">
  <h2>Settings:</h2>
</div>

## Main const:
Easy way to move all files.
Default:
``` js
const PATHS = {
  // Path to main app dir
  src: path.join(__dirname, '../src'),
  // Path to Output dir
  build: path.join(__dirname, '../build'),
  // Path to Second Output dir (js/css/fonts etc folder)
  assets: 'assets/'
}
```
## Customize:
Change any folders:
``` js
const PATHS = {
  // src must be src
  src: path.join(__dirname, '../src'),
  // build to public
  build: path.join(__dirname, '../public'),
  // assets to static
  assets: 'static/'
}
```

## Import Another libs:
1. Install libs
2. Import libs in `./index.js`
``` js
// React example
import React from 'react'
// Bootstrap example
import Bootstrap from 'bootstrap/dist/js/bootstrap.min.js'
import 'bootstrap/dist/js/bootstrap.min.js'
```

## Import only SASS or CSS libs:
1. Install libs
2. Go to `/assets/scss/utils/libs.scss`
3. Import libs in node modules
``` scss
// Sass librarys example:
@import '../../node_modules/spinners/stylesheets/spinners';
// CSS librarys example:
@import '../../node_modules/flickity/dist/flickity.css';
```

## Import js files:
1. Create another js module in `./js/` folder
2. Import modules in `./js/index.js` file
``` js
// another js file for example
import './common.js'
```

## HTML Dir Folder:
#### Default:
* .html dir: `./src`
* Configurations: in `./webpack-configs/webpack.base.conf.js`
``` js
const PAGES_DIR = PATHS.src
```
**Usage:**
All files must be created in the `./src` folder.
Example:
``` bash
./src/index.html
./src/about.html
```

#### Change HTML Default Dir Folder:
Example for `./src/pages`:
1. Create folder for all html files in `./src`. Be like: `./src/pages`
2. Change `./webpack-configs/webpack.base.conf.js` const PAGES_DIR:
``` js
// Old path
// const PAGES_DIR = PATHS.src

// Your new path
const PAGES_DIR = `${PATHS.src}/pages`
```
3. Rerun webpack dev server


**Usage:**
All files must be created in the `./src/pages` folder.
Example:
``` bash
./src/pages/index.html
./src/pages/about.html
```

## Create Another HTML Files:
#### Default: 
Automatic creation any html pages:
1. Create another html file in `./src` (main folder)
2. Open new page `http://localhost:8081/about.html` (Don't forget to RERUN dev server)

#### Second method:
Manual (not Automaticlly) creation any html pages (Don't forget to RERUN dev server and COMMENT lines above)
1. Create another html file in `./src` (main folder)
2. Go to `./webpack-configs/webpack.base.conf.js`
3. Comment lines above (create automaticlly html pages)
4. Create new page in html:
``` js
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/index.html`,
      filename: './index.html',
    }),
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/another.html`,
      filename: './another.html',
    }),
```
5. Open new page `http://localhost:8081/about.html` (Don't forget to RERUN dev server)

#### Third method: (BEST)
Сombine the first method and the second.
Example:
``` js
    ...PAGES.map(page => new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/${page}`,
      filename: `./${page}`
    })),
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/about/index.html`,
      filename: './about/index.html',
    }),
    new HtmlWebpackPlugin({
      template: `${PAGES_DIR}/about/portfolio.html`,
      filename: './about/portfolio.html',
    }),
```

Ideas: [Evgenii Vedegis](https://github.com/vedees)