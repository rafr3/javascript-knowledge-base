## Frontend developer tools

1. Prototyping  
  - JSBin
  - JSFiddle
  - Codepen

2. Skeleton  
  - NPM
  - Yeoman - Scaffolding, helps kickstart new projects.
  - Bower - Package manager (frameworks, libraries, assets, utilities...)
  - Gulp / Grunt - JavaScript task runners, performing repetitive tasks (minification, compilation, unit testing, linting...)
  - Frameworks: Bootstrap / Foundation / Primer / Skeleton  

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
    - AngularJS
    - Node.js, jQuery, Dojo

  - HTML
    - Jade
    - Haml
    - Emmet

  - CSS
    - Sass - CSS with variables, nesting, mixins, inheritance...
    - Less
    - Methodology:
      - [BEM (Block Element Modifier)](https://css-tricks.com/bem-101/)
      - [ITCSS (Inverted Triangle CSS)](http://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731)
      - [OOCSS (Object Oriented CSS)](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
      - [SMACSS (Scalable and Modular Architecture for CSS)](https://smacss.com/)
      - DRY (Don't Repeat Yourself)

  - Frameworks
    - [Bootstrap](http://getbootstrap.com/)
    - [Foundation](http://foundation.zurb.com/)
    - [Material UI](https://github.com/callemall/material-ui)
    - [Pure.css](http://purecss.io/)
    - JavaScript
      - AngularJS
      - Ember
      - Meteor
      - React

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


### Mobile apps
[Apache Cordova](https://cordova.apache.org/) / [PhoneGap]
[Ionic Framework](http://ionicframework.com/)

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
