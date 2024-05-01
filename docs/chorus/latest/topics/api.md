# API

!!! note "Many API endpoints are yet to be implemented"
    
    Though Chorus strives to implement as many api endpoints as possible, we are nowhere near 100% api coverage.
    If an endpoint you'd like to use isn't implemented yet, [consider helping out the project and implementing it](https://github.com/polyphony-chat/chorus/discussions/401) :D

The main way clients interact with Spacebar-compatible servers is via their HTTP API.

Chorus provides high level bindings to this API, usually through relevant objects themselves.

For example: [POST `/channels/{channel_id}/messages` - Send message](https://docs.discord.sex/resources/message#create-message) becomes [`Message::send()`](https://docs.rs/chorus/latest/chorus/types/struct.Message.html#method.send).

If you aren't sure where an API route will be, consider looking through Chorus' API modules.

In the above example, we can see that [the route](https://docs.rs/chorus/latest/src/chorus/api/channels/messages.rs.html#20) is implemented on [`Message`](https://docs.rs/chorus/latest/chorus/types/struct.Message.html) in [`chorus::api::channels::messages`](https://docs.rs/chorus/latest/chorus/api/channels/messages/index.html), a similar path to the route itself (`/channels/../messages`). 

## API Documentation

Discord maintains some documentation of their API on [their official developer portal](https://discord.com/developers/docs/reference),
though they mostly document bot account endpoints.

For the user API, some community made projects have attempted to document it:

- [Discord Userdoccers (aka. discord.sex)](https://docs.discord.sex/intro) - the single biggest source of Discord API knowledge, the reference for most of chorus' endpoints, though a few things are still missing

- [luna.gitlab.io (aka. discord-unofficial-docs)](https://luna.gitlab.io/discord-unofficial-docs/) - contains a few more obscure parts of the API, referenced in chorus for some user routes and gateway opcode 14

For Spacebar only routes or to see if a route is implemented in Spacebar, see [their OpenAPI spec](https://docs.spacebar.chat/routes).
