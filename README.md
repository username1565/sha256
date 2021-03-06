# A small SHA-256 implementation for JavaScript

The goals of this project are:
* small size  - the minified version is only 849 bytes
* readability - the unminified code should be relatively easy to understand/review

Input must be an ASCII string - if character codes outside the range 0-255 are received, `undefined` is returned.

## In the browser

The code (`sha256.js` or `sha256.min.js`) defines the `sha256(string)` function, which returns the hexadecimal-encoded SHA-256 hash of the input string.

AMD is also supported - use `index.js` instead.

test.html:
```html
<!-- UNCOMMENT some strings to TEST different included scripts -->
<!--<script src="sha256.js"></script>-->
<!--<script src="sha256.min.js"></script>-->
<!--<script src="sha256_unicode.js"></script>-->
<script src="sha256_unicode.min.js"></script>

<script>
//run script with ASCII - passed for all scripts.
document.write(
	'\
		(sha256(\'abc\')\
		===\
		\'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad\'\
	) '
	+
	(
		sha256('abc')	//ASCII-string
		===
		'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad'
	)
); //sha256('abc') === 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad'

document.write('<br>');	//next string

//run script with UTF-8 - passed only for sha256_unicode.js or sha256_unicode.min.js, and filed for ASCII.
document.write(
	'(sha256(\'test_string_with_text. Unicode: 守护村子\')\
		===\
		\'00ad1ffe387a8e277b81ffa0211c41a67e4580839ed785eea84b751a9e4be546\'\
	) '
	+
	(
		sha256('test_string_with_text. Unicode: 守护村子')	//UTF-string
		===
		'00ad1ffe387a8e277b81ffa0211c41a67e4580839ed785eea84b751a9e4be546'
	)
); //sha256('test_string_with_text. Unicode: 守护村子') === '00ad1ffe387a8e277b81ffa0211c41a67e4580839ed785eea84b751a9e4be546'
</script>
```

## In Node/CommonJS

If you're on Node, you should probably use the version from the built-in [`crypto` module](http://nodejs.org/api/crypto.html#crypto_crypto_createhash_algorithm).

However, it is made available as a CommonJS module, including the source code for the minified version:

```javascript
var sha256 = require('tiny-sha256');

var jsCode = sha256.code + 'alert(sha256("hello!"));';
```

## License

This library is released as "public domain".  You can copy, modify, re-release and re-license, or incorporate into any other project without restriction of any kind.