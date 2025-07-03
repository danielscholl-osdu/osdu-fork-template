# Documentation

Documentation is written in Markdown from the `docs` folder. The
`src` folder contains the sources with the `.md` extension.

We have adopted [MkDocs](https://www.mkdocs.org/) with the Material theme as an open source solution to
build the documentation starting from Markdown format.

## Getting Started

### Prerequisites

Before you can work with the documentation locally, you need to install the required dependencies.

### Installation

#### Option 1: Using pip (Recommended)

Install the required MkDocs plugins:

```bash
pip install mkdocs mkdocs-material mkdocs-minify-plugin pymdown-extensions
```

#### Option 2: Using Docker

If you prefer to use Docker, no additional installation is required.

### Local Development

You can locally test the documentation in two ways:

- using Docker
- using `mkdocs` directly

In both cases, you should issue the commands inside the `docs` folder.

#### Using Docker

With Docker, you just need to execute the following command and point your
browser to `http://127.0.0.1:8000/`:

```bash
docker run --rm -v "$(pwd):$(pwd)" -w "$(pwd)" -p 8000:8000 \
    minidocks/mkdocs \
    mkdocs serve -a 0.0.0.0:8000
```

#### Using MkDocs Directly

If you have installed `mkdocs` directly in your workstation, you can simply run:

```bash
mkdocs serve
```

Even in this case, point your browser to `http://127.0.0.1:8000/`.

### Required Plugins

The documentation uses the following MkDocs plugins:

- **mkdocs-material**: Material Design theme for MkDocs
- **mkdocs-minify-plugin**: Minifies HTML output
- **pymdown-extensions**: Python Markdown extensions (required for emoji support)
- **search**: Built-in search functionality

The configuration also includes support for:

- **Mermaid diagrams**: For flowcharts and diagrams
- **Code highlighting**: Syntax highlighting with Pygments
- **Material icons and emojis**: Enhanced visual elements
- **Tabbed interfaces**: For organized content presentation

### Project Structure

```
docs/
├── src/                    # Markdown source files
│   ├── architecture/       # Architecture documentation
│   ├── concepts.md         # Core concepts
│   ├── decisions/          # Architecture Decision Records (ADRs)
│   ├── images/             # Images and assets
│   ├── workflows/          # Workflow documentation
│   └── index.md            # Home page
├── mkdocs.yml              # MkDocs configuration
└── README.md               # This file
```

### Writing Documentation

- Use standard Markdown syntax
- Place images in `src/images/`
- Follow existing structure for consistency
- Use Mermaid for diagrams when possible

### Quality Assurance

Before you submit a pull request for the documentation, you must have gone through the following steps:

1. **Local test**: Verify the documentation builds and displays correctly
2. **Spell check**: Run through the spell checker
3. **Link validation**: Ensure all internal and external links work
4. **Mobile compatibility**: Test on different screen sizes

### Building for Production

To build the static site for deployment:

```bash
mkdocs build
```

The built site will be available in the `site/` directory.

### Live Documentation

The documentation is automatically deployed to GitHub Pages at:
https://danielscholl-osdu.github.io/osdu-fork-template/

### Troubleshooting

**Common Issues:**

1. **Plugin not found errors**: Install missing plugins with `pip install <plugin-name>`
2. **Material extensions error**: Install `pymdown-extensions` for emoji and syntax highlighting support
3. **Permission errors**: Use `pip install --user` for user-local installation
4. **Port already in use**: Use `mkdocs serve -a 127.0.0.1:8001` for alternative port

**Getting Help:**

- Check the [MkDocs documentation](https://www.mkdocs.org/)
- Review the [Material theme documentation](https://squidfunk.github.io/mkdocs-material/)
- Open an issue in this repository for project-specific questions
