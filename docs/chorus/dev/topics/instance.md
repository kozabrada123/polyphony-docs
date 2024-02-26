# Instance

A Chorus [`Instance`](https://docs.rs/chorus/latest/chorus/instance/struct.Instance.html) struct represents a connection to a Spacebar compatible server.

To create it, you can either pass a single root instance url:

```rs
    let instance = Instance::new("https://example.com/")
        .await
        .expect("Failed to connect to the Spacebar server");
```

Or you can create a [`UrlBundle`](https://docs.rs/chorus/latest/chorus/struct.UrlBundle.html):

```rs
    let bundle = UrlBundle::new(
        "https://example.com/api".to_string(),
        "wss://example.com/".to_string(),
        "https://example.com/cdn".to_string(),
    );
    let instance = Instance::from_url_bundle(bundle)
        .await
        .expect("Failed to connect to the Spacebar server");
```

Afterwards, you can log in with a [`LoginSchema`](https://docs.rs/chorus/latest/chorus/types/struct.LoginSchema.html#):

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

or using a token;

```rs
let user = instance
    .login_with_token(String::from("NzM1MTkxMTA2NjA5NjczOTQ2.RaZ7wE.Wytex9ukfbd7l68PQTGBEscXO4z"))
    .await
    .expect("An error occurred during the login process");
```

## ChorusUser

Logging in or registering will provide you with a [ChorusUser](https://docs.rs/chorus/latest/chorus/instance/struct.ChorusUser.html).

This struct represents an authenticated user account on an instance.

It is used to provide auth to api routes that need it.
