## Frontend developer tools

1. Prototyping  
  - JSBin
  - JSFiddle
  - Codepen

2. Skeleton  
  - NPM
  - Yeoman
  - Gulp / Grunt
  - Bootstrap / Foundation / Primer / Skeleton  

3. Code  
  - Editor / IDE
    - Atom
    - Sublime
    - WebStorm
    - VisualStudio

  - JavaScript
    - [CoffeeScript](http://coffeescript.org/) / [TypeScript](http://www.typescriptlang.org/)
    - [Babel](https://babeljs.io/) - Allows to use new syntax, right now without
    waiting for  browser support.
    - [JS Libraries](https://en.wikipedia.org/wiki/List_of_JavaScript_libraries)

  - HTML
    - Jade
    - Haml
    - Emmet

  - CSS
    - Sass
    - Less

  - Other
    - require.js
    - browserify

4. Testing  
  - Karma
  - Jasmine
  - Mocha
  - Chai
  - Phantom

5. Debugging  
  - Chrome Developer tools
  - Firefox Developer Edition

6. Distribution  
  - Require.js
  - WebPack
  - NPM
  - Bower


---
Node / Browserify / Webpack

### Why you need a build system like GRUNT, GULP, BRUNCH for your website

What should a build system do
- Repetitive tasks
    - Concatenating JavaScript  
     Prevents to opening many request for downloading separate js files.
    - Prefixing CSS  
     border-radius: -moz... is unnecessary because build system will add prefix automatically
- Utilities
    - JSHint
    - Uglify (compress/minify) Javascript
- Local server
- Live Reload

Why is his good for you?

Page Speed
- Less file requests for page load
- Faster file requests

Development Workflow
- You can use cool technologies
- You can break code into multiple files
- Easier to avoid code conflicts
- You can avoid annoying, repetitive tasks

Popular build systems:  
GULP - GRUNT - BRUNCH

Gulp is newest
