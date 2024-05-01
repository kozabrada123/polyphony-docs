# Getting started

To get started with Chorus, import it into your project by adding the following to your `Cargo.toml` file:

```toml
[dependencies]
chorus = "0.15.0"
```

Depending on what you want to do with chorus, [there are several different crate features you may want to enable later](../topics/features.md), but we can stick with the default for now.

The heart of Chorus is its connection to a Spacebar compatible server.

To establish such a connection, use the [`Instance`](../topics/instance.md) struct.

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

To login, for example:

```rs
let login_schema = LoginSchema {
    login: "user@example.com".to_string(),
    password: "Correct-Horse-Battery-Staple".to_string(),
    ..Default::default()
};
let user = instance
    .login_account(login_schema)
    .await
    .expect("An error occurred during the login process");
```

This will create a [ChorusUser](../../topics/instance/#chorususer), which can be used to perform authenticated action on the server.
