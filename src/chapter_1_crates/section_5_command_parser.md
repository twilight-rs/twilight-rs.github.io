# Command Parser

The Command Parser is a basic parser for the Twilight ecosystem. We'll get this out
of the way first: it's not a framework, and it doesn't try to be.

The parser, for the most part, takes a configuration of prefixes and commands,
and attempts to match it to provided strings, returning what command and prefix
it matched, if any. The parser will also return a lazy iterator of arguments
given to the command.

Included is a mutable configuration that allows you to specify the command
names, prefixes, and ignored guilds and users. The parser parses out commands
matching an available command and prefix and provides the command arguments to
you.

### Installation

Add the following to your Cargo.toml:

```toml
[dependencies]
twilight-command-parser = { git = "https://github.com/twilight-rs/twilight" }
```

### Examples

A simple parser for a bot with one prefix (`"!"`) and two commands, `"echo"`
and `"ping"`:

```rust
use twilight_command_parser::{Config, Output, Parser};

fn main() {
    let mut config = Config::new();
    
    // (Use `Config::add_command` to add a single command)
    config.add_command("echo");
    config.add_command("ping");
    
    // Add the prefix `"!"`.
    // (Use `Config::add_prefixes` to add multiple prefixes)
    config.add_prefix("!");
    
    let parser = Parser::new(config);
    
    // Now pass a command to the parser
    match parser.parse_str("!echo a message") {
        Output::Command { name: "echo", arguments, .. } => {
            let content = arguments.as_str();
    
            println!("Got an echo request to send `{}`", content);
        },
        Output::Command { name: "ping", .. } => {
            println!("Got a ping request");
        },
        Output::IgnoredGuild => println!("Message from ignored guild"),
        Output::IgnoredUser => println!("Message from ignored user"),
        Output::NoMatch => println!("Message didn't match a prefix and command"),
        // Ignore all other commands.
        _ => {},
    }
}
```

### Links

*source*: <https://github.com/twilight-rs/twilight/tree/master/command-parser>

*docs*: <https://docs.rs/twilight-command-parser>

*crates.io*: <https://crates.io/crates/twilight-command-parser>
