# @prantlf/astrobench

[![NPM version](https://badge.fury.io/js/%40prantlf%2Fastrobench.svg)](http://badge.fury.io/js/%40prantlf%2Fastrobench)
[![Dependency Status](https://david-dm.org/prantlf/astrobench.svg)](https://david-dm.org/prantlf/astrobench)
[![devDependency Status](https://david-dm.org/prantlf/astrobench/dev-status.svg)](https://david-dm.org/prantlf/astrobench#info=devDependencies)

> Make the Web Faster

JavaScript library for running in the browser performance benchmarks, based on Benchmark.js. Try the [live demo].

Easy way to create test cases. Provides rich and pretty UI.

[![astro.png][2]][1]

This fork enhances the original project with the following functionality:

* Includes the most recent version of `Benchmark.js`.
* Publishes minified script and stylesheet to reduce page loading times.
* Offers global functions `beforeBench` `afterBench`, `beforeSuite` and `afterSuite` to register setup and teardown callbacks for the tests.
* Allows command-line usage via [astrobench-cli].

## With Installation

Make sure that you have [NodeJS] >= 8 installed. Install `astrobench` with [npm] or [yarn]:

```
npm i @prantlf/astrobench
yarn add @prantlf/astrobench
```

## Without Installation

Instead of installing the package locally, you can load the script and stylesheet in the example below from [unpkg]. The URLs will look like this:

```html
<link rel="stylesheet"
      href="https://unpkg.com/@prantlf/astrobench@1.0.0/dist/astrobench.min.css">
<script src="https://unpkg.com/@prantlf/astrobench@1.0.0/dist/astrobench.min.js"></script>
```

## Usage

Create a HTML file in the directory where you installed the package, or anywhere using the URLs from [unpkg] above:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Performance Tests</title>
  <link rel="stylesheet" href="node_modules/@prantlf/astrobench/dist/astrobench.min.css">
</head>
<body>
  <!-- Wrapper for tests -->
  <div id="astrobench"></div>

  <script src="node_modules/@prantlf/astrobench/dist/astrobench.min.js"></script>
  <script>
    // A test suite begins with a call to the global function `suite`
    // with two parameters: a string and a function.
    // The string is a name or title for a spec suite – usually what is being
    // tested. The function is a block of code that implements the suite.
    suite('String matching', function(suite) {
      var text;

      // To help a test suite DRY up any duplicated setup code, provides
      // the global `beforeBench` functions. As the name implies,
      // this function is called once before each benchmark is executed.
      // You can store data in `suite` Object, or define necessary variables.
      // Code from body of the functions will be presented in UI.
      beforeBench(function() {
        suite.text = 'Hello world';
        text = 'Hello world';
      });

      // Benchmarks are defined by calling the global function `bench`,
      // which, like `suite` takes a string and a function.
      // The string is the title of the test and the function is the test.
      bench('String#match', function() {
        !! text.match(/o/);
      });

      bench('RegExp#test', function() {
        !! /o/.test(suite.text);
      });

      // Async benchmark.
      // Calls to `bench` can take an optional single argument, Deferred object,
      // method .resolve() should be called when the async work is complete.
      bench('Async#test', function(deferred) {
        setTimeout(function() {
          deferred.resolve();
        }, 100);
      },
      // Options for current benchmark
      // See more on http://benchmarkjs.com/docs#options
      {
        defer: true
      });
    });
  </script>
</body>
</html>
```

And enjoy the result.

[![sample.png][3]][1]

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding
style.  Add unit tests for any new or changed functionality. Lint and test
your code using Grunt.

## License

Copyright (c) 2020 Ferdinand Prantl

Licensed under the MIT license.

[1]: http://prantlf.github.com/astrobench/
[2]: https://prantlf.github.io/astrobench/astro.png
[3]: https://prantlf.github.io/astrobench/sample.png
[unpkg]: https://unpkg.com
[live demo]: http://prantlf.github.com/astrobench/
[astrobench-cli]: https://www.npmjs.com/package/astrobench-cli
[NodeJS]: http://nodejs.org/
[npm]: https://www.npmjs.org/
[yarn]: https://yarnpkg.com/
