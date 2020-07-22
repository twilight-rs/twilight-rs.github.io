# Gateway

`twilight-gateway` is an implementation of a client over Discord's websocket
gateway.

The main type is the `Shard`: it connects to the gateway, receives messages,
parses and processes them, and then gives them to you. It will automatically
reconnect, resume, and identify, as well as do some additional connectivity
checks.

Also provided is the `Cluster`, which will automatically manage a collection of
shards and unify their messages into one stream. It doesn't have a large API, you
usually want to spawn a task to bring it up such that you can begin to receive
tasks as soon as they arrive.

```rust
let cluster = Cluster::new(config).await?;

let mut events = cluster.events().await;

let cluster_spawn = cluster.clone();

tokio::spawn(async move {
    cluster_spawn.up().await;
});
```

### Installation

This library requires at least Rust 1.39+.

Add the following to your `Cargo.toml`:

```toml
twilight-gateway = { branch = "trunk", git = "https://github.com/twilight-rs/twilight" }
```

### Features

`twilight-gateway` includes only a feature: `simd-json`.

`simd-json` feature enables [simd-json] support to use simd features of the modern cpus
to deserialize json data faster. It is not enabled by default since not every cpu has those features.
To use this feature you need to also add these lines to a file in `<project root>/.cargo/config`
```toml
[build]
rustflags = ["-C", "target-cpu=native"]
```
you can also use this environment variable `RUSTFLAGS="-C target-cpu=native"`.

### Example

Starting a `Shard` and printing the contents of new messages as they come in:

```rust
use futures::StreamExt;
use std::{env, error::Error};
use twilight_gateway::Shard;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    // Initialize the tracing subscriber.
    tracing_subscriber::fmt::init();

    let mut shard = Shard::new(env::var("DISCORD_TOKEN")?);
    let mut events = shard.events().await;

    shard.start().await?;
    println!("Created shard");

    while let Some(event) = events.next().await {
        println!("Event: {:?}", event);
    }

    Ok(())
}
```

### Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/gateway>

*docs*: <https://twilight-rs.github.io/twilight/twilight_gateway/index.html>

*crates.io*: <https://crates.io/crates/twilight-gateway>

[img:shard]: ./section_3_shard.png
