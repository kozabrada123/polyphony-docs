# Getting started

To get started with Chorus, import it into your project by adding the following to your `Cargo.toml` file:

```toml
[dependencies]
chorus = "0.14.0"
```

The heart of Chorus is the connection to a Spacebar compatible server.

To establish such a connection, use the [`Instance`](https://docs.rs/chorus/latest/chorus/instance/struct.Instance.html) struct.

First, create the Instance:

```rs
use chorus::instance::Instance;

#[tokio::main]
async fn main() {
    let instance = Instance::new("https://example.com/")
        .await
        .expect("Failed to connect to the Spacebar server");
    // You can create as many instances of `Instance` as you want, but each `Instance` should likely be unique.
    dbg!(instance.instance_info);
    dbg!(instance.limits_information);
}
```

Now you can use this struct to login and register users on the server.


