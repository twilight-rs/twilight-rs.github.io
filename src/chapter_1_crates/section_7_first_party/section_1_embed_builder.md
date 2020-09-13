# Embed Builder

`twilight-embed-builder` is a utility crate to create validated embeds, useful
when creating or updating messages.

With this library, you can create mentions for various types, such as users,
emojis, roles, members, or channels.

## Installation

Add the following to your `Cargo.toml`:

```toml
twilight-embed-builder = "0.1"
```

## Examples

Build a simple embed:

```rust
use twilight_embed_builder::{EmbedBuilder, EmbedFieldBuilder};

let embed = EmbedBuilder::new()
    .description("Here's a list of reasons why Twilight is the best pony:")?
    .field(EmbedFieldBuilder::new("Wings", "She has wings.")?.inline())
    .field(EmbedFieldBuilder::new("Horn", "She can do magic, and she's really good at it.")?.inline())
    .build();
```

Build an embed with an image:

```rust
use twilight_embed_builder::{EmbedBuilder, ImageSource};

let embed = EmbedBuilder::new()
    .description("Here's a cool image of Twilight Sparkle")?
    .image(ImageSource::attachment("bestpony.png")?)
    .build();
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/utils/embed-builder>

*docs*: <https://twilight-rs.github.io/twilight/twilight_embed_builder/index.html>

*crates.io*: <https://crates.io/crates/twilight-embed-builder>
