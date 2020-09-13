# Standby

Standby is a utility to wait for an event to happen based on a predicate check.
For example, you may have a command that makes a reaction menu of ✅ and ❌. If
you want to handle a reaction to these, using something like an
application-level state or event stream may not suit your use case. It may be
cleaner to wait for a reaction inline to your function. This is where Standby
comes in.

## Installation

Add the following to your `Cargo.toml`:

```toml
twilight-standby = "0.1"
```

## Examples

Wait for a message in channel 123 by user 456 with the content "test":

```rust
use twilight_model::{gateway::payload::MessageCreate, id::{ChannelId, UserId}};
use twilight_standby::Standby;

let standby = Standby::new();

// Later on in the application...
let message = standby.wait_for_message(ChannelId(123), |event: &MessageCreate| {
    event.author.id == UserId(456) && event.content == "test"
}).await?;
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/standby>

*docs*: <https://twilight-rs.github.io/twilight/twilight_standby/index.html>

*crates.io*: <https://crates.io/crates/twilight-standby>
