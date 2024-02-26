# Gateway

The [Gateway](https://docs.discord.sex/topics/gateway) is the Spacebar protocol's way of providing real-time updates to clients, such as [notifying that a message was sent in a relevant server](https://docs.rs/chorus/latest/chorus/types/struct.MessageCreate.html) or [that someone is calling the local user](https://docs.rs/chorus/latest/chorus/types/struct.CallCreate.html).

These updates from the server are called events.

We'll touch on how to handle them later.

The gateway isn't used just for receiving events either - clients also send events for certain things, such as updating [their status](https://docs.rs/chorus/latest/chorus/types/struct.UpdatePresence.html) or [voice state (muted, defeaned, ...)](https://docs.rs/chorus/latest/chorus/types/struct.UpdateVoiceState.html).

## In Chorus

Chorus provides its own api for the gateway through the [`GatewayHandle`](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html), which is included in all instances of [`ChorusUser`](https://docs.rs/chorus/latest/chorus/instance/struct.ChorusUser.html).

(You can also manually create a handle through [`Gateway::spawn`](https://docs.rs/chorus/latest/chorus/gateway/gateway/struct.Gateway.html), but [you will need to manually authenticate](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html#method.send_identify).)

One handle links to one gateway connection, which is useful for one authenticated user.

Handles can be freely cloned and still correspond to the same connection.

### Receiving events

Chorus exposes receiving gateway events through the [`Observer` trait](https://docs.rs/chorus/latest/chorus/gateway/trait.Observer.html) and [`Events`](https://docs.rs/chorus/latest/chorus/gateway/gateway/event/struct.Events.html) struct.

The gateway's `Events` can be accessed through `GatewayHandle.events`.

For a real example of how to use Observers, see [`examples/gateway_observers.rs`](https://github.com/polyphony-chat/chorus/blob/dev/examples/gateway_observers.rs).

### Sending events

You can send gateway events using the [`send_*` functions](https://docs.rs/chorus/latest/chorus/gateway/handle/struct.GatewayHandle.html#implementations) in the `GatewayHandle`.
