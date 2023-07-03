Downloaded live sass compiler by glenn mark
Then open settings.json -> at the end type
    ", live.sass.compiler formatter" --> will have several options inside it
        change "expanded" to "compressed"
        savePath - null to "/dist"
        save it and close
to have watch sass option at the bottom, press crtl + p and f1 and type watch sass

Have a main "app" folder, in that two main folders
    - js -- contains script.js
    - scss -- contains style.scss and globals folder 
        globals folder contains > _boilerplate.scss, _index.scss, _typography.scss

    style.scss contains the style from globals or any other folder created in scss folder, and includes those in it by using @forward 'foldername', here 'globals'

    _boilerplate.scss contains basic style for the web pages
    _typography.scss contains the font styles to be used
    _index.scss contains the code of the _boilerplate.scss file and the _typography.scss file usign @forward '_boilerplate.scss'; format


have a dist folder on the same directory as app
    - contains style.css and style.css.map files

    In style.css.map file, do not type anything manually, it will include the code automatically when you have your code in .scss file and click "watch scss" option at the bottom

custom css variables:
    for example: we can use the rgb or hsl or hex values of colors as names of the variables, where the color value is stored in it.
    here, in colors.scss file --> 
        start from --> :root {
            --background-color: hsl(0, 0, 0);
        }

        to use this in other files, you need to write
            text-color: var(--background-color);

Sass Variables:

for fonts and stuff, make a new folder called "util" which is in same directory as globals folder, util directory contains two files _fonts.scss and _index.scss files.
where _fonts.scss is included in _index.scss using @foward method

in _fonts.scss file, write:
    $font: 'Open Sans', sans-serif;

    and use this $font in any other file needed

    for example if we need it in out bolierplate.scss file, we have to use "@use '../util' as u" instead of using forward method in main style.scss file

    to access those fonts, you have to write:
        font-family: u.$font; (in case you don't want to use u.$font, specify "as *" instead of "as u")

The next is the layout folder, which determines the the desktop or mobile or tablet layout --> The layout folder contains two files, they are:
        _grid.scss and _index.scss files (grid included in index.scss)
        include the layout folder in main style.scss

            * In _grid.scss, all the grid classes styling are included.
            * In index.html, the naming of classes is different, it uses BEM technique instead, i.e., for example class="grid__main" or "grid__sidebar"(two underscores in between)

            * In grid.scss, write the main class .grid {display: grid, ..
            
            &__main && &__sidebar { (the main class grid is selected, and inside it the sub-classes or the child classes are selected and rather than writing the main class name, it can just be written as &"rest of the name with underscore")
                ...
            }

            }

            * Include the media queries of it in grid class itself

setting widths: 
    1. min-width
    2. max-width
    3. in util folder -> new file named _breakpoints.scss which includes the breakpoints for different size of devices. For example, 


        $breakpoints-up: (
            "medium": 43.75em
            "large": 56.25em // 900 / 16
            "xlarge": 90rem
        );

    @mixin breakpoint {
        @media (min-width: map-get($breakpoints-up, $size)) {
        @content;
        }   

    }

same for breakpoint-down

to use these in diffren files, fist include util folder in the file using @use method'

in the file where you want to use these breakpoints, write the following:
    @include u.breakpoint-down(large) {
            text-align: left;
    }

70vw - viewport width (vw)

instead of using the above @include, you can use the following: 
    font-size: calc(16px + 2vw); 