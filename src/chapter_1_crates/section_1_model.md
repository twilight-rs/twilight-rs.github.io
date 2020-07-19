# Model

`twilight-model` is a crate of only serde models defining the Discord APIs with
no implementations on top of them and the amount of methods is very limited.

These are in a single crate for ease of use, a single point of definition,
and a sort of versioning of the Discord API. Similar to how a database
schema progresses in versions, the definition of the API also progresses in
versions.

The types in this crate are reproducible: deserializing a payload into a
type, serializing it, and then deserializing it again will work.

Defined are a number of modules defining types returned by or owned by
resource categories. For example, `gateway` are types used to interact with
and returned by the gateway API. `guild` contains types owned by the Guild
resource category. These types may be directly returned by, built on top of,
or extended by other crates.

### Installation

This crate requires Rust 1.31+.

Add the following to your `Cargo.toml`:

```toml
twilight-model = { git = "https://github.com/twilight-rs/twilight", branch = "trunk" }
```

### Features

The `simd-json` feature enables simd-json support to use simd features of 
the modern cpus to deserialize responses faster. It is not enabled by default.

To use this feature you need to also add these 
lines to `<project root>/.cargo/config`:

```toml
[build]
rustflags = ["-C", "target-cpu=native"]
```

You can also set the environment variable `RUSTFLAGS="-C target-cpu=native"`. 


### Links

*source*: <https://github.com/twilight-rs/twilight/tree/master/model>

*docs*: <https://twilight-rs.github.io/twilight/twilight_model/index.html>

*crates.io*: <https://crates.io/crates/twilight-model>
