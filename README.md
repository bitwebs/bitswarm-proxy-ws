# bitswarm-proxy-ws
Proxy bitswarm connections over websockets with auto-reconnect logic

```
npm -s @web4/bitswarm-proxy-ws
```

Uses the [bitswarm-proxy](https://github.com/bitwebs/bitswarm-proxy) module.

## Example

```js

const BitswarmServer = require('@web4/bitswarm-proxy-ws/server')

// Initialize the proxy server
// Also specify any options for bitswarm here
// https://github.com/bitwebs/bitswarm
const server = new BitswarmServer()

// Start listening on clients via websocket protocol
server.listen(3472)


const BitswarmClient = require('@web4/bitswarm-proxy-ws/client')

// Initialize a proxied bitswarm
// Also specify any options for bitswarm-proxy client
// https://github.com/bitwebs/bitswarm-proxy#client
const swarm = new BitswarmClient({
  // Specify a list of proxy servers available to connect to
	proxy: ['ws://127.0.0.1:3472']
})

// Same as with bitswarm
swarm.on('connection', (connection, info) => {
	const stream = getSomeStream(info.topic)

	// Pipe the data somewhere
	// E.G. bitdrive.replicate()
	connection.pipe(stream).pipe(connection)
})

swarm.join(topic)

swarm.leave(topic)
```
