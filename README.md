# shot

Injects a fake HTTP request/response into a node HTTP server for simulating server logic, writing tests, or debugging. Does not use a socket
connection so can be run against an inactive server (server not in listen mode).

[![Build Status](https://travis-ci.org/hapijs/shot.svg?branch=v3-commercial)](https://travis-ci.org/hapijs/shot)

## License

This version of the package requires a commercial license. You may not use, copy, or distribute it without first acquiring a commercial license from Sideway Inc. Using this software without a license is a violation of US and international law. To obtain a license, please contact [sales@sideway.com](mailto:sales@sideway.com). The open source version of this package can be found [here](https://github.com/hapijs/shot).

## Example

```javascript
// Load modules

const Http = require('http');
const Shot = require('shot');


// Declare internals

const internals = {};


internals.main = function () {

    const dispatch = function (req, res) {

        const reply = 'Hello World';
        res.writeHead(200, { 'Content-Type': 'text/plain', 'Content-Length': reply.length });
        res.end(reply);
    };

    const server = Http.createServer(dispatch);

    Shot.inject(dispatch, { method: 'get', url: '/' }, (res) => {

        console.log(res.payload);
    });
};


internals.main();
```

Note how `server.listen` is never called.

## API

See the [API Reference](API.md)
