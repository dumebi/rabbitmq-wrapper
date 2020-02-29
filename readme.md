


How to use this wrapper
```
const subscriber = require('@dumebi/rabbitmq-wrapper')
const publisher = require('@dumebi/rabbitmq-wrapper')
```

Setting up a connection
```
async function publish() {
  try {
    publisher.init(config.amqp_url);
  } catch (error) {
    console.log('RabbitMQ connection unsuccessful, retry after 5 seconds.')
    setTimeout(publish, 5000)
  }
}

async function subscribe() {
  try {
    subscriber.init(config.amqp_url);
  } catch (error) {
    console.log('RabbitMQ subscriber connection unsuccessful, retry after 5 seconds.')
    setTimeout(subscribe, 5000)
  }
}
```
publish an event

```
publisher.queue('QUEUE_NAME', { message })
```

consume an event

```
subscriber.consume('QUEUE_NAME', async (msg) => {
    try {
      const data = JSON.parse(msg.content.toString());
      const message = data.message
      subscriber.acknowledgeMessage(msg);
    } catch (error) {}
  }, 3);
```

you can always look through for better explanation
