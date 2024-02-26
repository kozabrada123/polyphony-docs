# Api

!!! note "Many api endpoints are yet to be implemented"
    
    Though Chorus strives to implement as many api endpoints as possible, we are nowhere near 100% api coverage.
    If an endpoint you'd like to use isn't implemented yet, [consider helping out the project and implementing it](https://github.com/polyphony-chat/chorus/discussions/401) :D

The main way to interact with Spacebar-compatible servers is using their http api.

Chorus provides high level bindings to this api, usually through relevant objects themselves.

For example: [POST `/channels/{channel_id}/messages` - Send message](https://docs.discord.sex/resources/message#create-message) becomes [`Message::send()`](https://docs.rs/chorus/latest/chorus/types/struct.Message.html#method.send).

If you aren't sure where an api route will be, consider looking through Chorus' api modules.

In the above example, we can see that [the route](https://docs.rs/chorus/latest/src/chorus/api/channels/messages.rs.html#20) is implemented on [`Message`](https://docs.rs/chorus/latest/chorus/types/struct.Message.html) in [`chorus::api::channels::messages`](https://docs.rs/chorus/latest/chorus/api/channels/messages/index.html), a similar path to the route itself (`/channels/../messages`). 
