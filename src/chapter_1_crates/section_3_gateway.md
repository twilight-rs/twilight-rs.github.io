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

```rust,no_run
# use futures::StreamExt;
# use twilight_gateway::Cluster;
#
# #[tokio::main]
# async fn main() -> Result<(), Box<dyn std::error::Error>> {
#    let token = "dummy";
let cluster = Cluster::new(token).await?;

let mut events = cluster.events();

let cluster_spawn = cluster.clone();

tokio::spawn(async move {
    cluster_spawn.up().await;
});
# let _ = events.next().await;
#     Ok(())
# }
```

## Features

`twilight-gateway` includes a few features `simd-json` for enabling faster json
parsing and `stock-zlib`/`simd-zlib` for choosing between the zlib to use for
decompressing.

### Simd JSON

`simd-json` feature enables [simd-json] support to use simd features of the modern cpus
to deserialize json data faster. It is not enabled by default since not every cpu has those features.
To use this feature you need to also add these lines to a file in `<project root>/.cargo/config`
```toml
[build]
rustflags = ["-C", "target-cpu=native"]
```
You can also use the environment variable `RUSTFLAGS="-C target-cpu=native"`.

### Zlib

`stock-zlib` makes [flate2] use the stock-zlib which is either upstream or the
one included with the operating system.

`simd-zlib` enables the use of [zlib-ng] which is a modern fork of zlib that in
most cases will be more effective. Though it will add an externel dependency on
[cmake].

If both are enabled or if the `zlib` feature of [flate2] is enabled anywhere in
the dependency tree it will make use of that instead of [zlib-ng].

## Example

Starting a `Shard` and printing the contents of new messages as they come in:

```rust,no_run
use futures::StreamExt;
use std::{env, error::Error};
use twilight_gateway::Shard;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    // Initialize the tracing subscriber.
    tracing_subscriber::fmt::init();

    let mut shard = Shard::new(env::var("DISCORD_TOKEN")?);
    let mut events = shard.events();

    shard.start().await?;
    println!("Created shard");

    while let Some(event) = events.next().await {
        println!("Event: {:?}", event);
    }

    Ok(())
}
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/gateway>

*docs*: <https://twilight-rs.github.io/twilight/twilight_gateway/index.html>

*crates.io*: <https://crates.io/crates/twilight-gateway>

[img:shard]: ./section_3_shard.png
[cmake]: https://cmake.org/
[flate2]: https://github.com/alexcrichton/flate2-rs
[zlib-ng]: https://github.com/zlib-ng/zlib-ng
