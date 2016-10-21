# rehype-format [![Build Status][travis-badge]][travis] [![Coverage Status][codecov-badge]][codecov]

Format HTML with [**rehype**][rehype].

## Installation

[npm][]:

```bash
npm install rehype-format
```

## Usage

Say we have the following file, `index.html`:

```html
<!doCTYPE HTML><html>
 <head>
    <title>Hello!</title>
<meta charset=utf8>
      </head>
  <body><section>    <p>hi there</p>
     </section>
 </body>
</html>
```

And our script, `example.js`, looks as follows:

```javascript
var vfile = require('to-vfile');
var report = require('vfile-reporter');
var rehype = require('rehype');
var format = require('rehype-format');

rehype().use(format).process(vfile.readSync('index.html'), function (err, file) {
  console.error(report(err || file));
  console.log(String(file));
});
```

Now, running `node example` yields:

```html
index.html: no issues found
<!DOCTYPE html>
<html>
  <head>
    <title>Hello!</title>
    <meta charset="utf8">
  </head>
  <body>
    <section>
      <p>hi there</p>
    </section>
  </body>
</html>
```

## API

### `rehype().use(format[, options])`

Format white-space in the processed tree.

*   Collapse all white-space (to a single space or newline);
*   Remove unneeded white-space;
*   Inject needed newlines and indentation;
*   Indent previously collapsed newlines properly.

All superfluous white-space is removed.  However, as newlines
are kept (and later properly indented), your code will still
line-wrap as expected.

###### `options`

*   `indent` (`number`, `string`, default: `2`)
    — Indentation per level.  When number, uses that amount
    of spaces.  When `string`, uses that per indentation
    level.
*   `indentInitial` (`boolean`, default: `true`)
    — Whether to indent the first level (usually, in the
    `html` element, thus not indenting `head` and `body`).
*   `blanks` (`Array.<string>`, default: `[]`)
    — List of tag-names, which, when next to each other,
    are joined by a blank line (`\n\n`).  For example,
    when `['head', 'body']` is given, a blank line is added
    between these two.

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definitions -->

[travis-badge]: https://img.shields.io/travis/wooorm/rehype-format.svg

[travis]: https://travis-ci.org/wooorm/rehype-format

[codecov-badge]: https://img.shields.io/codecov/c/github/wooorm/rehype-format.svg

[codecov]: https://codecov.io/github/wooorm/rehype-format

[npm]: https://docs.npmjs.com/cli/install

[license]: LICENSE

[author]: http://wooorm.com

[rehype]: https://github.com/wooorm/rehype
