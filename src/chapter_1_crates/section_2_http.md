# HTTP

`twilight-http` is an HTTP client wrapping all of the documented Discord HTTP API.
It is built on top of [Reqwest], and supports taking any generic Reqwest client,
allowing you to pick your own TLS backend. By default, it uses [RusTLS] a Rust TLS implementation,
but it can be changed to use NativeTLS which uses the TLS native to the platform, and on Unix uses OpenSSL.

Ratelimiting is included out-of-the-box, along with support for proxies.

## Installation

Add the following to your `Cargo.toml`:

```toml
twilight-http = { git = "https://github.com/twilight-rs/twilight" }
```

## Example

A quick example showing how to send 10 messages, and then print the current
user's name:

```rust
use futures::future;
use std::{env, error::Error};
use twilight_http::Client;
use twilight_model::id::ChannelId;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    // Initialize the tracing subscriber.
    tracing_subscriber::fmt::init();

    let client = Client::new(env::var("DISCORD_TOKEN")?);
    let channel_id = ChannelId(381_926_291_785_383_946);

    future::join_all((1u8..=10).map(|x| {
        client
            .create_message(channel_id)
            .content(format!("Ping #{}", x))
            .expect("content not a valid length")
    }))
    .await;

    let me = client.current_user().await?;
    println!("Current user: {}#{}", me.name, me.discriminator);

    Ok(())
}
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/http>

*docs*: <https://twilight-rs.github.io/twilight/twilight_http/index.html>

*crates.io*: <https://crates.io/crates/twilight-http>


[Reqwest]: https://github.com/seanmonstar/reqwest
[RusTLS]: https://github.com/ctz/rustls
