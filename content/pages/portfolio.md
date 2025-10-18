+++
title = "Portfolio"
template = "page.html"
+++

Here are a couple of projects I’ve created or contributed to.

# intervals-search

Natural-language search for [intervals.icu](https://intervals.icu) workout data using OpenRouter's LLM API.
Ask "show me hard bike rides from last month" and get filtered results.

**Tech stack**: FastAPI, React, OpenRouter (gpt-5-mini), intervals.icu API

**Why I built it**: Wanted to explore LLM integration patterns and MCP.
Also served as a reminder that I prefer backend development - I had Claude write all the CSS.

[Code](https://github.com/aidengindin/intervals-search)

# Homelab

Mini PC running NixOS with Caddy reverse proxy, DNS server, Immich, Miniflux, Calibre, and other services.
Plus a Raspberry Pi running Home Assistant OS.
My [NixOS configuration](https://github.com/aidengindin/nixos-config) is highly modular and shared across multiple devices - the home server, my laptop, and formerly my Steam Deck.

**Key features**:
- Declarative management under version control for full reproducibility
- Secrets (DB passwords, API keys) managed centrally with agenix
- Services accessible only over a Tailscale VPN, with Caddy providing HTTPS
- Automated backups via Restic

**Why it matters**:
When I break something during a rebuild (which is rare), Nix makes rollback trivial.
Outside of my own mistakes, uptime has been 100%.

# Personal website

This site is built with [Zola](https://www.getzola.org/) and the [Terminimal theme](https://github.com/pawroman/zola-theme-terminimal), featuring automated deployment to AWS S3.
Key technical aspects:

- **CI/CD Pipeline**: GitHub Actions workflow that automatically builds and deploys on pushes to main
- **Infrastructure**: 
  - S3 bucket configured for static website hosting with public access
  - Route 53 for DNS management
  - ACM for SSL certificate management
  - IAM roles and policies configured following principle of least privilege
  - Cloudfront for content delivery and HTTPS
- **Development**: 
  - Content written in Markdown
  - Local development using Nix flake for reproducible dev environment and consistent Zola versions
  - Git submodules for theme management
  - Favicon generated using DALL-E 3

Building this site didn't require any programming, but it was a chance for me to practice my DevOps skills.
While the source code doesn't contain anything too interesting, it's publicly available on [GitHub](https://github.com/aidengindin/personal-website).

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


# Imperative language interpreter

For a class on programming languages (CSDS 345), I worked in a small group to create an interpreter for a simple imperative language in Scheme.
It supports functions (including nested function definitions), break and continue from loops, and try/catch/finally blocks, and has limited support for objects.
The interpreter is purely functional, with program state passed as an argument between functions; tail recursion keeps stack size in check.
Because it was a class project, I’m not able to post the source code publicly, but it is available upon request.

# HTTP web server

As part of a networks class (CSDS 425), I built a basic HTTP/1.1 web server in Java with support for persistent connections.
Because it was a class project, I’m not able to post the source code publicly, but it is available upon request.

# Simple traceroute

For the same networks class, I built a simple traceroute tool in Python to measure the number of hops to a remote host.
Like the HTTP server, I can’t post the source code publicly, but it is available upon request.

