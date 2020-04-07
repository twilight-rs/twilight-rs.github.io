# Gateway

`twilight-gateway` is an implementation of a client over Discord's websocket
gateway.

The main type is the `Shard`: it connects to the gateway, receives messages,
parses and processes them, and then gives them to you. It will automatically
reconnect, resume, and identify, as well as do some additional connectivity
checks.

Also provided is the `Cluster`, which will automatically manage a collection of
shards and unify their messages into one stream. It doesn't have a large API --
pretty much just `up` and `down` to bring the cluster up or down. It implements
a stream which returns items of the ID of the shard a message came from, and the
parsed event representing it.

![Shard example][img:shard]

### Installation

This library requires at least Rust 1.39+.

Add the following to your `Cargo.toml`:

```toml
twilight-gateway = { git = "https://github.com/twilight-rs/twilight" }
```

### Example

Starting a `Shard` and printing the contents of new messages as they come in:

```rust
use futures::StreamExt;
use twilight::gateway::{Config, Event, Shard};
use std::{
    env,
    error::Error,
};

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Sync + Send>> {
    let token = env::var("DISCORD_TOKEN")?;
    
    let config = Config::builder(&token).build();
    let mut shard = Shard::new(config);
    shard.connect().await?;
    let mut events = shard.events();
    
    while let Some(event) = events.next().await {
        match event {
            Event::Connected(connected) => {
                println!("Connected on shard {}", connected.shard_id);
            },
            Event::Message(msg) => {
                if msg.content == "!ping" {
                    http.send_message(msg.channel_id).content("Pong!").await?;
                }
            },
            _ => {},
        }
    }
}
```

### Links

*source*: <https://github.com/twilight-rs/twilight/tree/master/gateway>

*docs*: <https://docs.rs/twilight-gateway>

*crates.io*: <https://crates.io/crates/twilight-gateway>

[img:shard]: ./section_3_shard.png
