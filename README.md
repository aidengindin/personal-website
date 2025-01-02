# Personal Website

My personal website, built with [Zola](https://www.getzola.org/) and the [Terminimal theme](https://github.com/pawroman/zola-theme-terminimal/).

## Development

This site uses Nix flakes for reproducible development environments. To get started:

1. Install Nix with flakes enabled
2. Install [direnv](https://direnv.net/) and [nix-direnv](https://github.com/nix-community/nix-direnv)
3. Run `direnv allow` to enter the development environment (this will happen automatically when you open a terminal in the project directory later)
4. Run `zola serve` to start the development server

## License

This repository contains two types of content with different licenses:

- All content in the `content/` directory (blog posts, pages, etc.) is licensed under [Creative Commons Attribution 4.0 International](content/LICENSE)
- All other files (templates, configuration, build scripts) are licensed under the [MIT License](LICENSE) 
