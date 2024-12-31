+++
title = "Portfolio"
template = "page.html"
+++

Here are a couple of projects I’ve created or contributed to.

# KineticAI

My main focus at the moment, [KineticAI](https://github.com/aidengindin/KineticAI) is a showcase project combining my passion for endurance sports with data integration and analysis.
Using a microservices architecture, the application loads data from third-party APIs into a database and performs various analytics, including weather impact modeling, AI-based sentiment analysis, and race prediction.
While KineticAI is still in early development and I’m still working on implementing most of its planned features, I’m excited to bring my data engineering skills to one of my hobbies and built something I can get real value out of.

# gpm-to-spotify

When Google announced they were shutting down Google Play Music, I realized that I would have to find another music streaming service.
Spotify was the only other one with a Linux desktop client, so the choice was easy.
But there was no way for me to transfer my library from GPM to Spotify without paying some random third party.
I figured that if both services had APIs, how hard could it be to do it myself?
(Famous last words…)
And thus, [gpm-to-spotify](https://github.com/aidengindin/gpm-to-spotfy) was born.

This is probably the ugliest, hackiest project I’ve worked on that’s actually worked.
It started as a bash script, but then I realized GPM’s (third-party) API only had Python bindings, so that part had to be spun out into Python.
Then, on the Spotify side, I realized as I worked on the project that it would need more API calls and error handling than I’d initially accounted for.
Rather than refactor my code, I just indented my code and debugged errors as they came up.
([Coding horror!](https://blog.codinghorror.com/))

Mistakes were made, and lessons were learned!
Granted, this was far from a production app - I was creating this solely for myself, the GPM side was read-only, and since I had no existing data in Spotify I could just remove everything when I messed up.
But if I were to start again, I’d do this very differently.
I’d write the whole thing as a Python script and split out the script’s functionality into smaller functions, making the code much more readable and debuggable.

# Homelab

I have a mini PC running NixOS serving a Caddy reverse proxy, a DNS server, Immich, FreshRSS, Calibre, and a few other services, plus a Raspberry Pi running Home Assistant OS.
My [NixOS configuration](https://github.com/aidengindin/nixos-config) is designed to be highly modular and shared across multiple devices; it’s used by both the home server and my MacBook, and for a while it ran on my Steam Deck, too.
This allows me to have a consistent setup across all my devices, and makes setting up new devices a breeze.
Services are configured as a mix of native NixOS modules and Nix-defined Docker containers, though in the past I’ve used Docker Compose.
While I’ve occasionally taken the server down by rebuilding with a bad configuration, Nix makes it easy to roll back to a working configuration, and outside of rebuilds the server has been 100% reliable.

A few of my favorite parts of the setup:

- The setup is as declarative as possible, with nearly all application configuration under version control, ensuring reproducibility
- Secrets such as database passwords and API keys are centrally managed using agenix
- All services are only accessible over Tailscale, with Caddy adding HTTPS support
- I’ve overridden the [Caddy derivation](https://github.com/aidengindin/nixos-config/blob/main/services/caddy.nix) to add support for Cloudflare, which enables automatic HTTPS for all services
- Restic backs up application data

(I love Home Assistant, too, but I haven’t done enough with it to merit inclusion on my portfolio page.)

# Imperative language interpreter

For a class on programming languages (CSDS 345), I worked in a small group to create an interpreter for a simple imperative language in Scheme.
It supports functions (including nested function definitions), break and continue from loops, and try/catch/finally blocks, and has limited support for objects.
The interpreter is purely functional, with program state passed as an argument between functions; tail recursion keeps stack size in check.
Because it was a class project, I’m not able to post the source code publicly, but it is available upon request.

# HTTP web server

As part of a networks class (CSDS 425), I built a basic HTTP/1.1 web server in Java with support for persistent connections.
Because it was a class project, I’m not able to post the source code publicly, but it is available upon request.

# Recipes app

For my senior project at CWRU, I worked with a group to develop a web-based recipe management app using Angular and Firebase.
I focused primarily on creating Angular services to interface with the backend database.
Because it was a class project, I’m not able to post the source code publicly, but it is available upon request.

# Simple traceroute

For the same networks class, I built a simple traceroute tool in Python to measure the number of hops to a remote host.
Like the HTTP server, I can’t post the source code publicly, but it is available upon request.

Want to see more? Check out my [GitHub profile](https://github.com/aidengindin) or [contact me](/pages/contact) to discuss potential collaborations. 