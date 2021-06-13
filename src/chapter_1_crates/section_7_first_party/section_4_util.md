# Util

`twilight-util` is a utility crate that adds utilities to the twilight
ecosystem that do not fit in any other crate. One example feature of the crate
is a trait to make extracting data from Discord identifiers (snowflakes) easier.

## Features

`twilight-util` by default exports nothing. Features must be individually
enabled via feature flags.

### Link

The `link` feature enables the parsing and formatting of URLs to resources, such
as parsing and formatting webhook links or links to a user's avatar.

#### Examples

Parse a webhook URL with a token:

```rust,no_run
# #[allow(unused_variables)]
# fn main() -> Result<(), Box<dyn std::error::Error>> {
use twilight_model::id::WebhookId;
use twilight_util::link::webhook;

let url = "https://discord.com/api/webhooks/794590023369752587/tjxHaPHLKp9aEdSwJuLeHhHHGEqIxt1aay4I67FOP9uzsYEWmj0eJmDn-2ZvCYLyOb_K";

let (id, token) = webhook::parse(url)?;
assert_eq!(WebhookId(794590023369752587), id);
assert_eq!(
    Some("tjxHaPHLKp9aEdSwJuLeHhHHGEqIxt1aay4I67FOP9uzsYEWmj0eJmDn-2ZvCYLyOb_K"),
    token,
);
# Ok(()) }
```

### Snowflake

The `snowflake` feature calculates information out of snowflakes, such as the
timestamp or the ID of the worker that created it.

#### Examples

Retrieve the timestamp of a snowflake in milliseconds from the Unix epoch as a
64-bit integer:

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

*source*: <https://github.com/twilight-rs/twilight/tree/main/util>

*docs*: <https://docs.rs/twilight-util>

*crates.io*: <https://crates.io/crates/twilight-util>
