# A Simple Gulp4 - Browsersync - Sass quick settup
Quick settup a project use gulp 4 + browsersync + sass.



## Create project directory

```
mkdir a-simple-gulp4-browsersync-sass-quick-settup
```

```
cd a-simple-gulp4-browsersync-sass-quick-settup
```

## Create a package.json file in your project directory

```
npm init -y
```
This will guide you through giving your project a name, version, description, etc.

## Install the gulp command line utility

```
npm install gulp-cli --save-dev
```

## Install the gulp, gulp-sass, browser-sync package in your devDependencies

```
npm install gulp gulp-sass browser-sync --save-dev
```

## Create a gulpfile
Using your text editor, create a file named __gulpfile.js__ in your project root with these contents:

```javascript
const {watch, src, dest}        = require('gulp');
const browserSync = require('browser-sync').create();
const sass        = require('gulp-sass');

// Compile sass into CSS & auto-inject into browsers
const scss = () => {
    return src("scss/**/*.scss")
        .pipe(sass())
        .pipe(dest("dist/assets/css"))
        .pipe(browserSync.stream());
} 

exports.default = () => {
    // Static Server + watching scss/html files 
    browserSync.init({
        server: "./"
    });
    // Watch the files when the files have change
    watch('scss/**/*.scss', scss);
    watch("**/*.html").on('change', browserSync.reload);
}
```

## Test it
Run the gulp command in your project directory:

```
gulp
```
