# Preparation

You'll need a couple of things before you get started with your bot.

### Rust Setup

Dawn requires async/await support, which is currently in Beta in Rust and
expected to be released with Rust 1.39. To install it, you'll need [rustup]. If
you haven't installed it, you should.

Although it's in Beta, some of the crates in the async/await ecosystem currently
require nightly, so we'll go with that. Install the nightly toolchain:

```shell
$ rustup install nightly
```

Now you'll want to make a project for your bot:

```shell
$ cargo new bot-name && cd $_
```

To use nightly Rust, you need to set it to be used for your bot project's
directory:

```shell
$ rustup override set nightly
```

### Making a Bot User

> If you already know how to do this, feel free to skip to
> [Installing Dawn](#installing-dawn).

In the [Discord Developer Portal] you'll find a page with a list of your
applications. Odds are if you don't know how to make a bot user, you haven't
before, so this is probably empty.

In the top-right you'll see a blurple **New Application** button. Click it.

![New Application button][img:new-application]

You'll be asked to give your application a name. For the example, we're naming
the application **Kona**. It doesn't matter what you name it, and it can be
changed later.

![Name your bot][img:name]

Now you'll be taken to your new application's page. On the sidebar, click
**Bot**.

![Sidebar][img:sidebar]

Now you'll see a button to **Add a Bot**. Click it. It'll ask if you're
**really sure** if you want to do this. Yeah, you are sure.

![Build a bot][img:build-a-bot]

Finally, you have a bot user. You can change its avatar and its username, so
that's cool, but not really what we need to care about. What you'll need is the
token. This is what will allow you to connect your bot to Discord's APIs. To get
it, click **Copy**.

> **Note**: It's *very*, **very**, ***very*** important that you don't give this
> token to *anybody*. If anyone has your token, then they can spam guilds, ban
> users, leave all the guilds that the bot is in, burn your house down, and
> everything.

# Installing Dawn

> Since this guide assumes familiarity with Rust already, this guide won't
> explain how using Cargo works.

We're going to add `dawn` as a dependency, which is the root crate re-exporting
all of the core crates, such as the HTTP and gateway clients, the models,
and cache.

To do that, add the following to your `Cargo.toml` file:

```toml
[dependencies]
dawn = { git = "https://github.com/dawn-rs/dawn" }
```

Now you're all set to get programming! In the next chapter you'll learn how to
write a simple ping-pong mechanism and why it works.

[Discord Developer Portal]: https://discordapp.com/developers/applications/
[rustup]: https://rustup.rs
[img:build-a-bot]: ./section_1_build_a_bot.png
[img:name]: ./section_1_name.png
[img:new-application]: ./section_1_new_application.png
[img:sidebar]: ./section_1_sidebar.png
[img:token]: ./section_1_token.png
