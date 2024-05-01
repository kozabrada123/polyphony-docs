# Gateway

The [Gateway](https://docs.discord.sex/topics/gateway) is the Spacebar protocol's way of providing real-time updates to clients, such as [notifying that a message was sent in a relevant server](https://docs.rs/chorus/latest/chorus/types/struct.MessageCreate.html) or [that someone is calling the local user](https://docs.rs/chorus/latest/chorus/types/struct.CallCreate.html).

These updates from the server are called events.

The gateway isn't used just for receiving events either - clients also send events for certain things, such as updating [their status](https://docs.rs/chorus/latest/chorus/types/struct.UpdatePresence.html) or [voice state (muted, defeaned, ...)](https://docs.rs/chorus/latest/chorus/types/struct.UpdateVoiceState.html).

## In Chorus

Chorus provides its own api for the gateway through the [`GatewayHandle`](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html), which is included in all instances of [`ChorusUser`](https://docs.rs/chorus/latest/chorus/instance/struct.ChorusUser.html).

(You can also manually create a handle through [`Gateway::spawn`](https://docs.rs/chorus/latest/chorus/gateway/gateway/struct.Gateway.html), but [you will need to manually authenticate](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html#method.send_identify).)

One handle links to one gateway connection, which is used for one authenticated user.

Handles can be freely cloned and still correspond to the same connection.

### Receiving events

Chorus exposes receiving gateway events through the [`Observer` trait](https://docs.rs/chorus/latest/chorus/gateway/trait.Observer.html) and [`Events`](https://docs.rs/chorus/latest/chorus/gateway/gateway/event/struct.Events.html) struct.

(The gateway's `Events` can be accessed through `GatewayHandle.events`.)

An Observer is a type which can be subscribed to certain events.

When that event happens or is received, the observer will execute its callback.

Here's an example:

```rs
...

// Due to certain limitations all observers must impl debug
#[derive(Debug)]
pub struct ExampleObserver {}

// This struct can observe GatewayReady events when subscribed, because it implements the trait Observer<GatewayReady>.
// The Observer trait can be implemented for a struct for a given websocketevent to handle observing it
// One struct can be an observer of multiple events, if needed
#[async_trait]
impl Observer<GatewayReady> for ExampleObserver {
    // After we subscribe to the event this function is called every time we receive it
    async fn update(&self, _data: &GatewayReady) {
        println!("Observed Ready!");
    }
}

#[tokio::main]
async fn main() {
    ...
    let gateway = ...;

    let observer = ExampleObserver {};

    // Share ownership of the observer with the gateway
    let shared_observer = Arc::new(observer);
    
    // Subscribe our observer to the Ready event on this gateway
    // From now on observer.update(data) will be called every time we receive the Ready event
    gateway
        .events
        .lock()
        .await
        .session
        .ready
        .subscribe(shared_observer);

    ... 
}

```

For the full code of this example, see [`examples/gateway_observers.rs`](https://github.com/polyphony-chat/chorus/blob/dev/examples/gateway_observers.rs).

### Sending events

You can send gateway events using the [`send_*` functions](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html#implementations) in the `GatewayHandle`.

For example, sending the [`Identify`](https://docs.rs/chorus/latest/chorus/types/struct.GatewayIdentifyPayload.html) event:

```rs
...

#[tokio::main]
async fn main() {
    let gateway = ...;

    // Create an identify event
    // An Identify event is how the server authenticates us and gets info about our os and browser, along with our intents / capabilities
    // (Chorus never sends real telemetry data about your system to servers, always just using the most common option or a custom set one)
    // By default the capabilities requests all the data of a regular client
    let mut identify = GatewayIdentifyPayload::common();

    identify.token = ...;

    // Send off the event
    gateway.send_identify(identify).await;
    ...
}

```

For the full code of this example, see [`examples/gateway_simple.rs`](https://github.com/polyphony-chat/chorus/blob/dev/examples/gateway_simple.rs).


