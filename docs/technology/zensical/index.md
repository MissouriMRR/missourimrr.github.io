# Zensical

This website was built using [Zensical](https://zensical.org/), a static site generator that turns a folder of [Markdown](markdown) files into a documentation site. Everything you see on the website lives in the `docs/` folder of the repository, and the site's settings and navigation live in `zensical.toml`.

## Editing an Existing Page

The easiest way to do this is to find the edit/pencil button at the top right of any page. This will bring you to the edit view of the associated file on GitHub, where you can make changes and preview them.

If you are modifying the site locally:

1. Find the file in `docs/`. The URL path matches the file path, so `/technology/git/` should be around `docs/technology/git.md`.
2. Edit the Markdown and save.
3. Check the result in the local preview.

These files are written in the Markdown format, which allows you to write in plain text, but there are more advanced features available like lists, code blocks, images, and more. See the [Markdown](markdown.md) page for a cheatsheet on everything you can do with Markdown.

Zensical also expands on Markdown with a couple of it's own features, which you can learn more about in the [Zensical documentation](https://zensical.org/docs/get-started/).

## Adding a New Page

1. **Create a new Markdown file:** Add a `.md` file in the folder where it belongs, for example `docs/technology/docker/docker.md`. Use lowercase names with underscores instead of spaces.
2. **Write a title:** Start the file with a single top-level heading (using one hashtag):

    ```markdown
    # Docker

    ... writing here ...
    ```

3. **Add it to the navigation settings:** Open `zensical.toml` and add an entry to the `nav` list. A page is only shown in the sidebar if it is listed there. Make sure to put it under the appropriate category:

    ```toml
    { "Technology" = [
      "technology/index.md",
      { "Docker" = "technology/docker.md" },
      # ...
    ]},
    ```

    The text on the left is the label shown in the sidebar, and the path on the right is relative to the `docs/` folder.

4. Preview it locally and make sure it appears where you expect it to be. Also check for any Zensical warnings/errors in the console.

### Adding a Section With Several Pages

To group pages, nest a list. Putting an `index.md` first makes it the section's landing page:

```toml
{ "Docker" = [
  "technology/docker/index.md",
  { "Installing Docker" = "technology/docker/install.md" },
  { "Compose" = "technology/docker/compose.md" },
]},
```

## Repository Layout

```
.
├── zensical.toml      # Site settings and navigation setup
└── docs/
    ├── index.md       # Home page
    ├── assets/        # Images
    ├── stylesheets/   # Custom CSS files (we use this to add the Multirotor green color, for example)
    └── technology/
        └── zensical/
            └── index.md   # This page
```

Each `.md` file under `docs/` becomes a page. Any `index.md` is the landing/base page for its folder/subfolder.

## Running/Hosting the Site Locally

Just like with most other Python projects made by the team, we use `uv` to create a development environment:
```bash
uv sync
```

You can then use the `zensical` CLI:
```bash
uv run zensical serve
```

This will start a local version of the site at `http://localhost:8000/`. It will automatically refresh when you make changes.
