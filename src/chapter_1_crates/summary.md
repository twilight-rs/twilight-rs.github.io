# Crates

Dawn is, at heart, an ecosystem. These components of the ecosystem generally,
for the most part, don't depend on each other. The crates in it are sectioned
into three "parts": the *core crates*, *first-party crates*, and *third-party
crates*.

### Core Crates

Dawn includes a few crates which are the "building blocks" to your success. You
might not need them all, but generally speaking you'll need most of them for
your use case. Most of them wrap Discord's various APIs.

- *model*: All of the structs, enums, and bitflags used by the Discord APIs.
- *http*: An HTTP client supporting all of the documented features of Discord's
  HTTP API, with support for ratelimiting, proxying, and more.
- *gateway*: A client supporting Discord's gateway API.
- *cache*: Definitions for implementating a cache. An in-process memory
  implementation is included.
- *voice*: A client supporting Discord's voice API.
- *command-parser*: A basic command parser for parsing commands and arguments
  out of messages.
- *dawn*: The root crate, re-exporting all of the other core crates in one
  unified crate.

### First-Party Crates

Additionally, there are some first-party crates maintained by the Dawn
organization, but not included in the core experience. These might be for more
advanced use cases or clients for third-party services. Two examples of
first-party crates are `dawn-cache-redis` - an implementation of a cache using
Redis as a backend - and `dawn-lavalink`, an implementation of a client for
Lavalink.

### Third-Party Crates

Third-party crates may start to exist over time. These aren't officially
supported by the Dawn organization, and are maintained by other people.

These are currently no third-party crates. I mean, this thing isn't even at 0.1
yet.

[Lavalink]: https://github.com/Frederikam/Lavalink
[redis]: https://redis.io
