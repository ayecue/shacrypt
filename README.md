[![Build Status](https://travis-ci.org/oleksiyk/shacrypt.png)](https://travis-ci.org/oleksiyk/shacrypt)

# shacrypt

shacrypt provides cross-platform support for SHA-256 crypt and SHA-512 crypt in Node.js. It does not use the Node.js crypto API. Instead, it is implemented as a Node.js addon that wraps around the [C implementation programmed by Ulrich Drepper](http://www.akkadia.org/drepper/SHA-crypt.txt). This provides significantly increased performance.

shacrypt provides two functions `sha256crypt()` and `sha512crypt()` that can be used both synchronously and asynchronously via callbacks.

Asynchronous mode is especially useful in that computation is performed in Node.js's libuv thread pool. This avoids blocking the event loop which results in better app responsiveness. As per Node.js convention, the callback function is provided as the final argument with the signature `function(error, result){}`.

### Installation

```
npm install vlasky/shacrypt
```

NOTE: You will need to have C++ build tools installed on your system to successfully install the package. If you are running under Windows, you can download Microsoft's [Build Tools for Visual Studio 2017](https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017).

### Usage
* Prerequisite

	```javascript
	var shacrypt = require('shacrypt');
	```
* Generate password hash:

	```javascript
	var hash = shacrypt.sha256crypt('super password');
	// hash = $5$rounds=5000$3a1afb28e54a0391$0d6RupbpABtxCaH8WWOemYwEcToDVZXX/tHpIy6O1U3
	```
* Validate password:

	```javascript
	console.log(hash == shacrypt.sha256crypt('super password', hash);
	// true
	```
* Specify number of rounds (default is 5000):

	```javascript
	var hash = shacrypt.sha256crypt('super password', 10000);
	// hash = $5$rounds=10000$b2c0a3ef466b2ec7$poVvVeQAQSE.yec0LBFddzQ9kZ4UxzA5VtsZQShAyt8
	```
* Provide your own SALT:

	```javascript
	var hash = shacrypt.sha256crypt('super password', 'my-salt');
	// or with iterations=10000
	var hash = shacrypt.sha256crypt('super password', 'my-salt', 10000);
	```

## Authors

* Vlad Lasky [https://github.com/vlasky](https://github.com/vlasky)
* Oleksiy Krivoshey [https://github.com/oleksiyk](https://github.com/oleksiyk)
* Original C code by Ulrich Drepper: <http://www.akkadia.org/drepper/SHA-crypt.txt>

# License (MIT)

Copyright (c) 2013-2015 Oleksiy Krivoshey.

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

