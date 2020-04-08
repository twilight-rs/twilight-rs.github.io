# Overview

<img
  src="https://raw.githubusercontent.com/twilight-rs/twilight/master/logo.png" 
  alt="twilight logo"
/>

[Join us on Discord! :)][server]

> **Warning**: Twilight is still a work in progress, so while some of this stuff
> exists *right now*, a lot of it doesn't. Features, APIs, and usage of crates
> not completed is documented for design feedback. You shouldn't try building
> something yet.

**twilight** is an ecosystem of asynchronous, unopinionated, and extensible
libraries for using the Discord APIs. It has the additional goals of simplicity,
fearless breaking changes where needed, and the embracing of third party
libraries.

### The Guide

In this guide you'll learn about the core crates in the twilight ecosystem, useful
first-party crates for more advanced use cases, and third-party crates giving
you a tailored experience. You'll build a bot using all of the core crates
available, and learn why and how to use services for larger bots.

### Links

The organization for the project is [on GitHub, named "twilight-rs"][github].

The crates are available on [crates.io].

The API docs are also hosted for the [latest version][docs:latest].

There is a community and support server [on Discord][server].

### A Quick Example

Below is a quick example of a program printing "Pong!" when a ping command comes
in from a channel:

```rust,ignore
use futures::StreamExt;
use twilight::{
    command_parser::{Command, Config as ParserConfig, Parser},
    gateway::{Config, Event, Shard},
};
use std::{
    env,
    error::Error,
};

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    let token = env::var("DISCORD_TOKEN")?;

    let shard = Shard::new(token).await?;

    let parser = {
        let mut config = Config::new();
        config.command("ping").add();
        config.add_prefix("!");
        Parser::new(config)
    };

    let mut events = shard.events().await;

    while let Some(event) = events.next().await {
        match event {
            Event::MessageCreate(msg) => match parser.parse(&msg.content) {
                Command { name: "ping", .. } => println!("Pong!"),
                _ => {},
            },
            _ => {},
        }
    }
}
```

[crates.io]: https://crates.io/crates/twilight
[docs:latest]: https://docs.rs/twilight
[github]: https://github.com/twilight-rs
[server]: https://discord.gg/WBdGJCc
