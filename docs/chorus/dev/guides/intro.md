# Intro

Chorus is a Rust library which poses as an API wrapper for [Spacebar Chat](https://github.com/spacebarchat/)
and Discord. It is designed to be easy to use, and to be compatible with both Discord and Spacebar Chat.

You can establish as many connections to as many servers as you want, and you can use them all at the same time.

Chorus combines all the required functionalities of a user-centric Spacebar library into one package. 
The library handles various aspects on your behalf, such as rate limiting, authentication and maintaining
a WebSocket connection to the Gateway. This means that you can focus on building your application,
instead of worrying about the underlying implementation details.

