# Overview

<img
  src="https://raw.githubusercontent.com/dawn-rs/dawn/master/logo.png" 
  alt="dawn logo"
/>

[Join us on Discord! :)][server]

> **Warning**: Dawn is still a work in progress, so while some of this stuff
> exists *right now*, a lot of it doesn't. Features, APIs, and usage of crates
> not completed is documented for design feedback. You shouldn't try building
> something yet.

**dawn** is an ecosystem of asynchronous, unopinionated, and extensible
libraries for using the Discord APIs. It has the additional goals of simplicity,
fearless breaking changes where needed, and the embracing of third party
libraries.

### The Guide

In this guide you'll learn about the core crates in the dawn ecosystem, useful
first-party crates for more advanced use cases, and third-party crates giving
you a tailored experience. You'll build a bot using all of the core crates
available, and learn why and how to use services for larger bots.

### Links

The organization for the project is [on GitHub, named "dawn-rs"][github].

The crates are available on [crates.io].

The API docs are also hosted for the [latest version][docs:latest].

There is a community and support server [on Discord][server].

If you need to email us for some reason (don't have a GitHub account, but don't
want to join the server?), then we can be reached at `dawn@valley.cafe`.

### A Quick Example

Below is a quick example of a program printing "Pong!" when a ping command comes
in from a channel:

```rust,ignore
use futures::StreamExt;
use dawn::{
    command_parser::Parser,
    gateway::{Config, Event, Shard},
};
use std::{
    env,
    error::Error,
};

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    let token = env::var("DISCORD_TOKEN")?;

    let parser = Parser::builder()
        .prefix("!")
        .command("ping")
        .build();

    let mut shard = Shard::builder(&token).build();
    shard.connect().await?;
    let mut events = shard.events();

    while let Some(event) = events.next().await {
        match event {
            Event::Message(msg) => match parser.parse(msg) {
                Output::Command { name: "ping", .. } => println!("Pong!"),
                _ => {},
            },
            _ => {},
        }
    }
}
```

[crates.io]: https://crates.io/crates/dawn
[docs:latest]: https://dawn-rs.github.io
[github]: https://github.com/dawn-rs
[server]: https://discord.gg/WBdGJCc
