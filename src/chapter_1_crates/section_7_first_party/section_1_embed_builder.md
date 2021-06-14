# Embed Builder

`twilight-embed-builder` is a utility crate to create validated embeds, useful
when creating or updating messages.

With this library, you can create mentions for various types, such as users,
emojis, roles, members, or channels.

## Examples

Build a simple embed:

```rust
# #[allow(unused_variables)]
# fn main() -> Result<(), Box<dyn std::error::Error>> {
use twilight_embed_builder::{EmbedBuilder, EmbedFieldBuilder};

let embed = EmbedBuilder::new()
    .description("Here's a list of reasons why Twilight is the best pony:")
    .field(EmbedFieldBuilder::new("Wings", "She has wings.").inline())
    .field(EmbedFieldBuilder::new("Horn", "She can do magic, and she's really good at it.").inline())
    .build()?;
#     Ok(())
# }
```

Build an embed with an image:

```rust
# #[allow(unused_variables)]
# fn main() -> Result<(), Box<dyn std::error::Error>> {
use twilight_embed_builder::{EmbedBuilder, ImageSource};

let embed = EmbedBuilder::new()
    .description("Here's a cool image of Twilight Sparkle")
    .image(ImageSource::attachment("bestpony.png")?)
    .build()?;
#     Ok(())
# }
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/main/utils/embed-builder>

*docs*: <https://docs.rs/twilight-embed-builder>

*crates.io*: <https://crates.io/crates/twilight-embed-builder>
