# Cache

Twilight includes an in-process-memory cache. It's responsible for processing
events and caching things like guilds, channels, users, and voice states.

## Installation

Add the following to your Cargo.toml:

```toml
[dependencies]
twilight-cache-inmemory = "0.1"
```

## Examples

Process items that come over a shard into the cache:

```rust
use futures::stream::StreamExt;
use std::env;
use twilight_cache_inmemory::InMemoryCache;
use twilight_gateway::Shard;

let token = env::var("DISCORD_TOKEN")?;

let shard = Shard::new(token);
shard.start().await?;

let cache = InMemoryCache::new();

let mut events = shard.events();

while let Some(event) = events.next().await {
    cache.process(&event);
}
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/cache/in-memory>

*docs*: <https://docs.rs/twilight-cache-inmemory>

*crates.io*: <https://crates.io/crates/twilight-cache-inmemory>
