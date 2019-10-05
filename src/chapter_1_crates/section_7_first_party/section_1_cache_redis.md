# Redis Cache

`dawn-cache-redis` is an implementation of a cache using Redis as a backend. It
is entirely stateless other than the TCP connection used by [`redis`] itself.

Read the section on [the cache crate] for more information on how this is
implemented.

### Example

Creating a connection to the redis database and getting a guild by ID:

```rust
use dawn_cache_redis::RedisCache;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    let cache = RedisCache::connect(("0.0.0.0", 6379)).await?;
    
    if let Some(guild) = cache.guild(620980184606048276).await? {
        println!("Guild name: {}", guild.name);
    }

    Ok(())
}
```

### Links

**source**: <https://github.com/dawn-rs/dawn/tree/master/cache/redis>
**docs**: <https://docs.rs/dawn-cache-redis>
**crates.io**: <https://crates.io/crates/dawn-cache-redis>

[`redis`]: https://docs.rs/redis
[the cache crate]: ../section_4_cache.html
