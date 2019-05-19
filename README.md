# gulp-sass-build
Streamlining theme development workflow with Omega, LibSass and Gulp

Workshop presented at: https://pnwdrupalsummit.org/2015/sessions/streamlining-theme-development-omega-libsass-and-gulp

The first time I used Drupal's Omega 4 theme what impressed me most was the magical "drush ogrd" command that not only automatically compiled my sass into css, but also reloaded my browser too! I called it magical because prior to using Omega typing "compass" on command line was my sass build process and now in comparison ogrd was indeed magic as I had no idea how it worked and all I cared about was the compiled results in my css folder. Omega's workflow worked great for a while until my sub-theme became increasingly complex and the compile and LiveReload process started to lag, forcing me to find a way to speed it up. My first attempt at speeding up sass processing was avoiding process heavy compass functions and by simply replacing a few background-image() calls which generate images from CSS3 gradients I cut my build time in nearly half.

Introducing LibSass
-------------------
Sass originated in the Ruby realm and as such it took a while for ports in other languages to catch up with the constant progress of the original Ruby branch, but at the cost of being slightly behind the bleeding edge the C port of Sass known as LibSass is solid and fast! As the name suggests LibSass is just a library and in order to compile Sass with it we still need to run an executable that uses this library...

SassC Time
----------
Once I got LibSass compiled I tested it with its sister app SassC, which was blazing fast. I made a "Watcher" process inside my PHPStorm IDE that compiled sass into css as fast as I typed, overkill of course, but a real build process includes more than just compiling css, post-css processing such as vendor-prefixes, or LiveReload refresh requests are needed!

Hello Gulp
----------
Omega 4 by default uses Grunt to run each task defined in the build process but there are drawbacks, Grunt is config-heavy, just take a look at your sub-theme's Gruntfile and you'll notice how at the end of each task files are saved to the disk only to be read back in by the next task. By replacing the temp file paradigm with an efficient "stream" passing through pipes not only is Gulp faster than Grunt but also easier to maintain as it requires less configuration.


Pros / Advantages
-----------------
Performence speed / Configuration legibility / Access to variables in layouts / Global access to Susy breakpoints.

Cons / Challenges
-----------------
Along the path there were a few snags, a pesky file order difference between Ruby's sass-globbing and Gulp's ran through the parent folder files before the partial folders resulting in undefined variable and mixin errors and forcing me to replicate the sass partial import order in gulp, repeating those 5 lines is not DRY coding but it works! Also stepping outside the default Omega norms and Keeping up with extra dependencies.
