# Util

`twilight-util` is a utility crate that adds utilities to the twilight
ecosystem that do not fit in any other crate. One example feature of the crate
is a trait to make extracting data from Discord identifiers (snowflakes) easier.

## Features

`twilight-util` by default exports nothing. Features must be individually
enabled via feature flags.

### Builder

The `builder` feature enables builders for large structs, at the
moment only a builder for commands is availible.

#### Examples

Create a command that can be used to send a animal picture in a
certain category:

```rust
# fn main() {
use twilight_model::application::command::CommandType;
use twilight_util::builder::command::{BooleanBuilder, CommandBuilder, StringBuilder};

CommandBuilder::new(
    "blep".into(),
    "Send a random adorable animal photo".into(),
    CommandType::ChatInput,
)
.option(
    StringBuilder::new("animal".into(), "The type of animal".into())
        .required(true)
        .choices([
            ("Dog".into(), "animal_dog".into()),
            ("Cat".into(), "animal_cat".into()),
            ("Penguin".into(), "animal_penguin".into()),
        ]),
)
.option(BooleanBuilder::new(
    "only_smol".into(),
    "Whether to show only baby animals".into(),
));
# }
```

### Link

The `link` feature enables the parsing and formatting of URLs to resources, such
as parsing and formatting webhook links or links to a user's avatar.

#### Examples

Parse a webhook URL with a token:

```rust,no_run
# #[allow(unused_variables)]
# fn main() -> Result<(), Box<dyn std::error::Error>> {
use twilight_model::id::Id;
use twilight_util::link::webhook;

let url = "https://discord.com/api/webhooks/794590023369752587/tjxHaPHLKp9aEdSwJuLeHhHHGEqIxt1aay4I67FOP9uzsYEWmj0eJmDn-2ZvCYLyOb_K";

let (id, token) = webhook::parse(url)?;
assert_eq!(Id::new(794590023369752587), id);
assert_eq!(
    Some("tjxHaPHLKp9aEdSwJuLeHhHHGEqIxt1aay4I67FOP9uzsYEWmj0eJmDn-2ZvCYLyOb_K"),
    token,
);
# Ok(()) }
```

### Permission Calculator

The `permission-calculator` feature is used for calculating the permissions
of a member in a channel, taking into account its roles and permission
overwrites.

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
use twilight_model::id::{Id, marker::UserMarker};

let user: Id<UserMarker> = Id::new(123456);
let timestamp = user.timestamp();
# }
```


## Links

*source*: <https://github.com/twilight-rs/twilight/tree/main/util>

*docs*: <https://docs.rs/twilight-util>

*crates.io*: <https://crates.io/crates/twilight-util>
