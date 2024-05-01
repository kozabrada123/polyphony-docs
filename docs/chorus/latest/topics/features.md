# Features

Chorus has several crate features:

| Feature                 | description                                                                                                                       |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| rt                      | Enables the tokio runtime                                                                                                         |
| rt-multi-thread \* \*\* | Enables the tokio multi-threaded runtime                                                                                          |
| client \*               | Enables features useful for building a client, such as the api, gateway, instance and ratelimiter                                 |
| backend                 | Enables features useful for building a backend, such as certain sqlx type support                                                 |
| voice \*\*              | Enables experimental voice support - same as enabling voice_udp and voice_gateway simultaneously                                  |
| voice_udp \*\*          | Enables support for receiving voice via discord's UDP api.                                                                        |
| voice_gateway           | Enables support for the voice gateway. Used to open and close voice connections, but useless without a way to receive voice data. |

\* - Feature is enabled by default

\*\* - Not available on WASM targets
