# Util

`twilight-util` is a utility crate that adds utilities to the twilight
ecosystem that do not fit in any other crate. Currently, it contains
a trait to make extracting data from Discord identifiers (Snowflakes)
easier.

## Examples
The snowflake trait can be used like this
```rust
# #[allow(unused_variables)]
# fn main() {
use twilight_util::snowflake::Snowflake;
use twilight_model::id::UserId;

let user = UserId(123456);
let timestamp = user.timestamp();
# }
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/util>

*docs*: <https://docs.rs/twilight-util>

*crates.io*: <https://crates.io/crates/twilight-util>
