# Model

`twilight-model` is a crate of models for use with [serde] defining the Discord
APIs with limited implementations on top of them.

These are in a single crate for ease of use, a single point of definition,
and a sort of versioning of the Discord API. Similar to how a database
schema progresses in versions, the definition of the API also progresses in
versions.

Most other Twilight crates use types from this crate. For example, the
[Embed Builder] crate primarily uses types having to do with channel message
embeds, while the [Lavalink] crate works with a few of the events received from
the gateway. These types being in a single versioned definition is beneficial
because it removes the need for crates to rely on other large and unnecessary
crates.

The types in this crate are reproducible: deserializing a payload into a
type, serializing it, and then deserializing it again will result in the same
instance.

Defined are a number of modules defining types returned by or owned by
resource categories. For example, `gateway` contains types used to interact with
and returned by the gateway API. `guild` contains types owned by the Guild
resource category. These types may be directly returned by, built on top of,
or extended by other Twilight crates.

## Installation

Add the following to your `Cargo.toml`:

```toml
twilight-model = "0.1"
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/master/model>

*docs*: <https://twilight-rs.github.io/twilight/twilight_model/index.html>

*crates.io*: <https://crates.io/crates/twilight-model>

[Embed Builder]: a
[Lavalink]: ./section_7_first_party/section_2_lavalink.md
[serde]: https://serde.rs/
