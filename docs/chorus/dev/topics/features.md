# Features

Chorus has multiple available crate features:

| Feature         | description                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------|
| rt              | Enable the tokio runtime                                                                          |
| rt-multi-thread | Enable the tokio multi-threaded runtime                                                           |
| client          | Enables features useful for building a client, such as the api, gateway, instance and ratelimiter |
| backend         | Enables features useful for building a backend, such as certain sqlx type support                 |

By default chorus enables features `client` and `rt-multi-thread`.

It should be noted that `rt-multi-thread` is not supported on WASM. 
