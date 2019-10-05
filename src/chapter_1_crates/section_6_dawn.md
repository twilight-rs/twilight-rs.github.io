# Dawn

`dawn` is the root crate of the entire project. It's what could be called a
"skeleton crate": all it does is re-export all of the other core crates.

Since all of the crates in Dawn are building blocks, they aren't very
intertwined. This means that they can be used separately without having to bring
in the entire ecosystem of core crates. Most people, though, will need all of
these crates. To create a single unified experience with easy installation, this
crate exists to provide all of them.

### Source Code

This is the entire contents of the library:

```rust
#[cfg(feature = "cache")]
pub extern crate dawn_cache as cache;

#[cfg(feature = "command-parser")]
pub extern crate dawn_command_parser as command_parser;

#[cfg(feature = "gateway")]
pub extern crate dawn_gateway as gateway;

#[cfg(feature = "http")]
pub extern crate dawn_http as http;

#[cfg(feature = "model")]
pub extern crate dawn_model as model;

#[cfg(feature = "voice")]
pub extern crate dawn_voice as voice;
```

### Installation

This library requires at least Rust 1.39+.

Add the following to your `Cargo.toml`:

```toml
dawn = { git = "https://github.com/dawn-rs/dawn" }
```

### Features

All of the crates that are re-exported can be disabled. For example, if you need
everything but `voice`, then you can disable only voice. This looks like:

```toml
[dependencies.dawn]
default-features = false
features = ["cache", "command-parser", "gateway", "http", "model"]
git = "https://github.com/dawn-rs/dawn"
```

This is the list of features, which are all enabled by default:

- `cache`
- `command-parser`
- `gateway`
- `http`
- `model`
- `voice`

If you're developing a library, it's easier for users to know what you depend on
by depending on the individual crates. If you're making a framework, this might
look like:

```toml
[dependencies]
dawn-cache = { git = "https://github.com/dawn-rs/dawn" }
dawn-gateway = { git = "https://github.com/dawn-rs/dawn" }
dawn-http = { git = "https://github.com/dawn-rs/dawn" }
```

### Links

*source*: <https://github.com/dawn-rs/dawn>

*docs*: <https://docs.rs/dawn>

*crates.io*: <https://crates.io/crates/dawn>
