# a-simple-gulp4-browsersync-sass-quick-settup
Quick settup a project use gulp 4 + browsersync + sass.

```
    npm install browser-sync gulp gulp-sass --save-dev
```

gulpfile.js

```javascript
const {watch, src, dest}        = require('gulp');
const browserSync = require('browser-sync').create();
const sass        = require('gulp-sass');

// Compile sass into CSS & auto-inject into browsers
const scss = () => {
    return src("scss/*.scss")
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
    watch('scss/*.scss', scss);
    watch("*.html").on('change', browserSync.reload);
}
```
