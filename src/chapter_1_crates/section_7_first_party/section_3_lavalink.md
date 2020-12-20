# Lavalink

`twilight-lavalink` is a client for [Lavalink] for use with [model] events from
the [gateway].

It includes support for managing multiple nodes, a player manager for
conveniently using players to send events and retrieve information for each
guild, and an HTTP module for creating requests using the http crate and
providing models to deserialize their responses.

## Examples

Create a [client], add a [node], and give events to the client to [process]
events:

```rust,no_run
use futures::StreamExt;
use std::{
    env,
    error::Error,
    net::SocketAddr,
    str::FromStr,
};
use twilight_gateway::Shard;
use twilight_http::Client as HttpClient;
use twilight_lavalink::Lavalink;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync + 'static>> {
    let token = env::var("DISCORD_TOKEN")?;
    let lavalink_host = SocketAddr::from_str(&env::var("LAVALINK_HOST")?)?;
    let lavalink_auth = env::var("LAVALINK_AUTHORIZATION")?;
    let shard_count = 1_u64;

    let http = HttpClient::new(&token);
    let user_id = http.current_user().await?.id;

    let lavalink = Lavalink::new(user_id, shard_count);
    lavalink.add(lavalink_host, lavalink_auth).await?;

    let mut shard = Shard::new(token);
    let mut events = shard.events();

    shard.start().await?;

    while let Some(event) = events.next().await {
        lavalink.process(&event).await?;
    }

    Ok(())
}
```

## Links

**source**: <https://github.com/twilight-rs/twilight/tree/trunk/lavalink>

**docs**: <https://docs.rs/twilight-lavalink>

**crates.io**: <https://crates.io/crates/twilight-lavalink>

[Lavalink]: https://github.com/Frederikam/Lavalink
[client]: https://twilight-rs.github.io/twilight/twilight_lavalink/client/struct.Lavalink.html
[gateway]: ../section_3_gateway.html
[model]: ../section_1_model.html
[node]: https://twilight-rs.github.io/twilight/twilight_lavalink/node/struct.Node.html
[process]: https://twilight-rs.github.io/twilight/twilight_lavalink/client/struct.Lavalink.html#method.process
