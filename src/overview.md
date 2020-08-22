# Overview

<img
  src="https://raw.githubusercontent.com/twilight-rs/twilight/trunk/logo.png"
  alt="twilight logo"
/>

[Join us on Discord! :)][server]

**twilight** is a powerful asynchronous, flexible, and scalable ecosystem of
Rust libraries for the Discord API.

[Check out the crates on crates.io][crates.io].

## Who Twilight is For

Twilight is meant for people who are very familiar with Rust and at least
somewhat familiar with Discord bots. It aims to be the library you use when you
want - or, maybe for scaling reasons, need - the freedom to structure things
how you want and do things that other libraries may not strongly cater to.

If you're a beginner with Rust, then that's cool and we hope you like it!
[serenity] is a great library for getting started and offers an opinionated,
batteries-included approach to making bots. You'll probably have a better
experience with it and we recommend you check it out.

## The Guide

In this guide you'll learn about the core crates in the twilight ecosystem,
useful first-party crates for more advanced use cases, and third-party crates
giving you a tailored experience.

## Links

The organization for the project is [on GitHub][github].

The crates are available on [crates.io].

The API docs are also hosted for the [latest version][docs:latest].

There is a community and support server [on Discord][server].

## A Quick Example

Below is a quick example of a program printing "Pong!" when a ping command comes
in from a channel:

```rust
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

    // Create a shard, which is the driver for an event loop over incoming
    // events and sending events.
    let mut shard = Shard::new(env::var("DISCORD_TOKEN")?);
    // Retrieve a new asynchronous stream of the events that the shard will
    // receive.
    let mut events = shard.events();

    let parser = {
        let mut config = Config::new();
        config.command("ping").add();
        config.add_prefix("!");
        Parser::new(config)
    };

    // Start the shard to begin receiving events.
    shard.start().await?;

    while let Some(event) = events.next().await {
        match event {
            Event::MessageCreate(msg) => match parser.parse(&msg.content) {
                Command { name: "ping", .. } => println!("Pong!"),
                _ => {},
            },
            // More events here...
            _ => {},
        }
    }
}
```

[crates.io]: https://crates.io/teams/github:twilight-rs:core
[docs:latest]: https://twilight-rs.github.io/twilight/
[github]: https://github.com/twilight-rs
[serenity]: https://crates.io/crates/serenity
[server]: https://discord.gg/7jj8n7D
