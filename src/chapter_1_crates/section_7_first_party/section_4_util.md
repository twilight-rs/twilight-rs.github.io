# Util

`twilight-util` is a utility crate that adds utilities to the twilight
ecosystem that do not fit in any other crate. Currently, it contains
a trait to make extracting data from Discord identifiers (Snowflakes)
easier.

## Installation

Add the following to your `Cargo.toml`:
```toml
twilight-util = { features = ["snowflake"], version = "0.1" }
```

## Examples
The snowflake trait can be used like this
```rust
use twilight_util::snowflake::Snowflake;
use twilight_model::id::UserId;

let user = UserId(123456);
let timestamp = user.timestamp();
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/util>

*docs*: <https://api.twilight.rs/twilight_util/index.html>

*crates.io*: <https://crates.io/crates/twilight-util>
