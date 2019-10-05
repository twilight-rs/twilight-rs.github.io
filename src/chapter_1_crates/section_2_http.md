# HTTP

`dawn-http` is an HTTP client wrapping all of the documented Discord HTTP API.
It is built on top of [Reqwest], and supports taking any generic Reqwest client,
allowing you to pick your own TLS backend. By default, it uses [RusTLS], a Rust
TLS implementation.

Ratelimiting is included out-of-the-box, along with support for proxies.

### Installation

This library requires at least Rust 1.39+.

Add the following to your `Cargo.toml`:

```toml
dawn-http = { git = "https://github.com/dawn-rs/dawn" }
```

### Example

A quick example showing how to send 10 messages, and then print the current
user's name:

```rust
use dawn::{
    http::Client,
    model::id::ChannelId,
};
use futures::future;
use std::{env, error::Error};

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    let client = Client::new(env::var("DISCORD_TOKEN")?);
    let channel_id = ChannelId(620980184606048278);

    future::join_all((1u8..=10).map(|x| {
        client.create_message(channel_id).content(format!("Ping #{}", x))
    })).await;

    let me = client.current_user().await?;
    println!("Current user: {}#{}", me.name, me.discriminator);

    Ok(())
}
```

### Links

*source*: <https://github.com/dawn-rs/dawn/tree/master/http>

*docs*: <https://docs.rs/dawn-http>

*crates.io*: <https://crates.io/crates/dawn-http>


[Reqwest]: https://github.com/seanmonstar/reqwest
[RusTLS]: https://github.com/ctz/rustls
