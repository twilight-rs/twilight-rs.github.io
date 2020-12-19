# Mention

`twilight-mention` is a utility crate to mention [model] resources.

With this library, you can create mentions for various resources, such as users,
emojis, roles, members, or channels.

## Installation

Add the following to your `Cargo.toml`:

```toml
twilight-mention = "0.1"
```

## Examples

Create a mention formatter for a user ID, and then format it in a message:

```rust
# #[allow(unused_variables)]
# fn main() {
use twilight_mention::Mention;
use twilight_model::id::UserId;

let user_id = UserId(123);
let message = format!("Hey there, {}!", user_id.mention());
# }
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/utils/mention>

*docs*: <https://docs.rs/twilight-mention>

*crates.io*: <https://crates.io/crates/twilight-mention>

[model]: ../section_1_model.html
