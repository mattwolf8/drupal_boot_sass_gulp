# drupal_boot_sass_gulp

## Create a Drupal7 Bootstrap SubTheme with Sass and gulp

####GET BOOTSTRAP COMPONENTS FOR DRUPAL
  Download the Bootstrap Theme

    https://www.drupal.org/project/bootstrap

  Download and enable the jquery_update module

    https://www.drupal.org/project/jquery_update
  
  Set the “Default jQuery Version” to 1.9 or above.


####CREATE THE SUBTHEME DIRECTORY
  Copy the LESS directory

    drupal/public/sites/all/themes/bootstrap/starterkits/less
  
  Paste the LESS directory

    sites/all/themes/
  
  Rename the LESS directory

    sites/all/themes/sub_theme

  Open the sub_theme directory

  Rename less.starterkit to sub_theme.info.

  Open sub_theme.info in an IDE. 
  
  Change the name to sub_theme
  
  Change the description and any other properties to suite your needs.

  Change Default theme to sub_theme in appearances


####REMOVE LESS COMPONENTS
  Navigate to the sub_theme directory

    sites/all/themes/sub_theme
  
  Delete the LESS directory
  
  In terminal navigate to the sub_theme directory

    $ sites/all/themes/sub_theme
  
  In terminal, create a sass directory

    $ mkdir sass
  
  Open the sass directory in terminal

    $ sites/all/themes/sub_theme/sass
  
  Create a style.scss file 

    $ touch style.scss

####GET BOOTSTRAP FOR SASS
  Download The Sass Version of Bootstrap

    https://github.com/twbs/bootstrap-sass/archive/v3.3.6.tar.gz
  
  Uncompress the archive
  
  Move the uncompressed directory to the sub_theme directory

    sites/all/themes/sub_theme/bootstrap-sass-3.3.6 
  
  Rename bootstrap-sass-3.3.6 to bootsrap

    sites/all/themes/sub_theme/bootstrap


####SETTING UP GULP
  In terminal, navigate to the sub_theme directory

    $ sites/all/themes/sub_theme
  
  Initialize NPM

    $ npm init

    (enter through the prompts)

  Open package.json with IDE

    /sub_theme/package.json 

  Change the scripts object from:

    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },  
  
  Change the scripts object to:

    "scripts": {
      "postinstall": "find node_modules/ -name '*.info' -type f -delete"
    },

  In terminal, navigate to the sub_theme directory

    $ sites/all/themes/sub_theme

  create a file called .npmrc

    $ touch .npmrc

  open .npmrc

    $ nano .npmrc

  add the following 

    $ unsafe-perm = true

  Save and Exit Nano

    $ ^x
    $ Y

  Open the package.json file in an IDE  and add the following:
    
    {
      "name": "sub_theme",
      "version": "1.0.0",
      "description": "<!-- @file Instructions for subtheming using the LESS Starterkit. --> <!-- @defgroup subtheme_less --> <!-- @ingroup subtheme --> # LESS Starterkit",
      "main": "index.js",
          "devDependencies": {
        "gulp": "^3.9.1",
        "gulp-autoprefixer": "^3.1.0",
        "gulp-sass": "^2.3.1"
      },
      "scripts": {
        "postinstall": "find node_modules/ -name '*.info' -type f -delete"
      },
      "author": "",
      "license": "ISC"
    }

  In terminal, navigate to the sub_theme directory

    $ sites/all/themes/sub_theme

  Run npm Install 

    $ npm install

  In the subtheme director, create the gulpfile.js 

    $ touch gulpfile.js

  In an IDE open gulpfile.js and add the following:

    var gulp = require('gulp');
    var sass = require('gulp-sass');
    var prefix = require('gulp-autoprefixer');

    gulp.task('hello', function() {
      console.log('Hello sub_theme builder');
    });

    gulp.task('sass', function(){
      return gulp.src('./sass/style.scss')
        // Converts Sass to CSS with gulp-sass
        // Adds auto-prefixer 
        .pipe(sass({
          outputStyle: 'expanded'
        }))
        .pipe(prefix('last 4 versions'))
        .pipe(gulp.dest('./css/'))
    });

    gulp.task('watch', function() {
        gulp.watch('sass/**/*.scss',['sass']);
    });

    gulp.task('default',['sass']);


  Navigate to the sub_theme directory in terminal

    $ sites/all/themes/sub_theme
  
  Execute the intial test

    $ gulp hello
  
  Navigate to the sub_theme directory in terminal

    $ sites/all/themes/sub_theme

  Run the Sass task

    $ gulp sass
  
  Open style.scss in an IDE and write the following test:

    .testing {
      width: percentage(5/7);
      display: flex; 
    }
  
  Navigate to the sub_theme/css/style.css file in an IDE.

 The file should contain:

      .testing {
        width: 71.42857%; 
        display: -webkit-flex;
        display: -ms-flexbox;
        display: flex;
      }

  From terminal, navigate to the sub_theme directory

    $ sites/all/themes/sub_theme

  Run the gulp watch task  
  (the style.css will be automatically updated when the scss file is changed)

    $ gulp watch


####LINKING BOOTSTRAP TO SASS
  Navigate to the sub_theme directory
  
  Open the sub_theme.info file in an IDE 
  
  Change the the Scripts to the following paths

    scripts[] = 'bootstrap/assets/javascripts/bootstrap/affix.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/alert.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/button.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/carousel.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/collapse.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/dropdown.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/modal.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/tooltip.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/popover.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/scrollspy.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/tab.js'
    scripts[] = 'bootstrap/assets/javascripts/bootstrap/transition.js'

  Navigate back to the sub_theme/sass directory 
  
  Open the style.scss file in an IDE
  
  Add to the top of the style.scss file 

    @import "../bootstrap/assets/stylesheets/bootstrap.scss";

  Navigate to sites/all/themes/sub_theme in terminal 

    $ sites/all/themes/sub_theme

  Navigate to the sub_theme/css/style.css 

    The file should now be populated with bootstrap Sass files

  If not, run the gulp sass task in terminal 

    $ gulp sass 

####Sources
  * [Chen Hui Jing](https://www.chenhuijing.com/blog/drupal-101-theming-with-gulp/)
  * [Drupal-Bootstrap-Subtheme](http://drupal-bootstrap.org/api/bootstrap/docs!subtheme!README.md/group/subtheme/7)
  * [Drupal-Bootstrap-Less](http://drupal-bootstrap.org/api/bootstrap/starterkits%21less%21README.md/group/subtheme_less/7)
  * [Create a Subtheme](http://www.zyxware.com/articles/5164/drupal-how-to-create-bootstrap-subtheme-in-drupal-7)
  * [Zell @ CSS Tricks](https://css-tricks.com/gulp-for-beginners/)

####Requirements:
  Drupal7

  NodeJS
