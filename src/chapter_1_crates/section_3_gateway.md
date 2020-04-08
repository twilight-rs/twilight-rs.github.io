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
use std::{env, error::Error};
use twilight_gateway::Shard;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    pretty_env_logger::init_timed();

    let shard = Shard::new(env::var("DISCORD_TOKEN")?).await?;
    println!("Created shard");

    let mut events = shard.events().await;

    while let Some(event) = events.next().await {
        println!("Event: {:?}", event);
    }

    Ok(())
}
```

### Links

*source*: <https://github.com/twilight-rs/twilight/tree/master/gateway>

*docs*: <https://docs.rs/twilight-gateway>

*crates.io*: <https://crates.io/crates/twilight-gateway>

[img:shard]: ./section_3_shard.png
