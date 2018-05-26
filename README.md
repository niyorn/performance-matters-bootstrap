# Performance matters
This project serve as a testing ground for different optimalisation technique. Each technique has their own branch where the technique is applied to the project to see if there's a increase in performance. The master branche contain all of the technique combined. 

The documentation for each technique can be found in the __AUDIT.md__ file.

## Project setup

This project serves an adapted version of the [Bootstrap documentation website](http://getbootstrap.com/). It is based on the [github pages branche of Bootstrap](https://github.com/twbs/bootstrap/tree/gh-pages). 

Differences from actual Bootstrap documentation:

- Added custom webfont
- Removed third party scripts
- The src directory is served with [Express](https://expressjs.com/).
- Templating is done with [Nunjucks](https://mozilla.github.io/nunjucks/)

## Getting started

- Install dependencies: `npm install`
- Serve: `npm start`
- Expose localhost: `npm run expose`