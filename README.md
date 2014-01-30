# qb-messageq

[messageq](https://github.com/rafflecopter/node-messageq) dialect for [qb](https://github.com/rafflecopter/node-qb)

## Usage

[messageq](https://github.com/Rafflecopter/node-messageq) is a simple, reliable Redis-backed task queue based pub/sub messaging system based on [relyq](https://github.com/Rafflecopter/relyq). It is based on a pub/sub model and an example follows.

```
npm install qb-messageq --save
```

```javascript
qb.speaks(require('qb-messageq'), { port: 8000, base: '/qb-api' })
  .start()

  // Access a channel using messageq and qb's `contact` polymethod
  .contact('messageq://new-users-channel')
    // Listen for messages on this channel
    .subscribe(function onNewUser(msg) {})
    // Or you can directly invoke a service queue
    .subscribe('service-to-execute-with-message');

// Or you can create an alias
qb.contacts('messageq://some-channel', 'some-channel')
  .contact('some-channel')
  // And lastly, you can publish on channels
  .publish({a: 'message', to: 'be', deliv:'ered'});
```

Options:

- `discovery_prefix: 'my-soa-discovery'` (required) - Redis key prefix for the discovery service. This must be same across all messageq instances that want to talk to each other.
- `ttl: 5000` (default: 5s (in ms)) - Time to live between cached subscriber requests. Use a large one for long-term subscribers.

Note: The messageq dialect will use the same redis server as the qb framework for task queuing.

## License

MIT in LICENSE file