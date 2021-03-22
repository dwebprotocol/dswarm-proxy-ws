# @dswarm/proxy-ws
Proxy dswarm connections over websockets with auto-reconnect logic

```
npm -s @dswarm/proxy-ws
```

Uses the [dswarm-proxy](https://github.com/dwebprotocol/dswarm-proxy) module.

## Example

```js

const DSwarmServer = require('@dswarm/proxy-ws/server')

// Initialize the proxy server
// Also specify any options for dswarm here
// https://github.com/dswarm/dswarm
const server = new DSwarmServer()

// Start listening on clients via websocket protocol
server.listen(3472)


const DSwarmClient = require('@dswarm/proxy-ws/client')

// Initialize a proxied dswarm
// Also specify any options for dswarm-proxy client
// https://github.com/dwebprotocol/dswarm-proxy#client
const swarm = new DSwarmClient({
  // Specify a list of proxy servers available to connect to
	proxy: ['ws://127.0.0.1:3472']
})

// Same as with dswarm
swarm.on('connection', (connection, info) => {
	const stream = getSomeStream(info.topic)

	// Pipe the data somewhere
	// E.G. ddrive.replicate()
	connection.pipe(stream).pipe(connection)
})

swarm.join(topic)

swarm.leave(topic)
```
