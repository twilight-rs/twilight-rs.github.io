# Twilight

`twilight` is the root crate of the entire project. It's what could be called a
"skeleton crate": all it does is re-export all of the other core crates.

Since all of the crates in Twilight are building blocks, they aren't very
intertwined. This means that they can be used separately without having to bring
in the entire ecosystem of core crates. Most people, though, will need all of
these crates. To create a single unified experience with easy installation, this
crate exists to provide all of them.

### Source Code

This is the entire contents of the library:

```rust
#[cfg(feature = "builders")]
pub extern crate twilight_builders as builders;

#[cfg(feature = "cache")]
pub extern crate twilight_cache as cache;

#[cfg(feature = "command-parser")]
pub extern crate twilight_command_parser as command_parser;

#[cfg(feature = "gateway")]
pub extern crate twilight_gateway as gateway;

#[cfg(feature = "http")]
pub extern crate twilight_http as http;

#[cfg(feature = "model")]
pub extern crate twilight_model as model;

#[cfg(feature = "standby")]
pub extern crate twilight_standby as standby;
```

### Installation

This library requires at least Rust 1.39+.

Add the following to your `Cargo.toml`:

```toml
twilight = { branch = "trunk", git = "https://github.com/twilight-rs/twilight" }
```

### Features

All of the crates that are re-exported can be disabled. For example, if you need
everything but `cache`, then you can disable only voice. This looks like:

```toml
[dependencies.twilight]
branch = "trunk"
default-features = false
features = ["command-parser", "gateway", "http", "model", "standby"]
git = "https://github.com/twilight-rs/twilight"
```

This is the list of features, which are all enabled by default:

- `cache`
- `command-parser`
- `gateway`
- `http`
- `model`
- `standby`

If you're developing a library, it's easier for users to know what you depend on
by depending on the individual crates. If you're making a framework, this might
look like:

```toml
[dependencies]
twilight-cache = { branch = "trunk", git = "https://github.com/twilight-rs/twilight" }
twilight-gateway = { branch = "trunk", git = "https://github.com/twilight-rs/twilight" }
twilight-http = { branch = "trunk", git = "https://github.com/twilight-rs/twilight" }
```

### Links

*source*: <https://github.com/twilight-rs/twilight>

*docs*: <https://twilight-rs.github.io/twilight/twilight/index.html>

*crates.io*: <https://crates.io/crates/twilight>
