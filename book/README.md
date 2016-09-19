We're using [GitBook][gitbook] for write-ups and documentation. It takes in Markdown files and spits out a nice-looking website, PDF, or EPUB. We periodically dump the web version on [GitHub Pages][gh-pages] (the `gh-pages` branch of this repository).

To use GitBook, install globally:

```bash
npm install -g gitbook-cli
```

We also require some dependencies (at the moment, only emoji). Those can also be installed via `npm`:

```bash
npm install
```

After GitBook and dependencies are installed,

*   Run a local, continuously rebuilding website with `gitbook serve`.
*   Build the site for distribution with `gitbook build`.
*   Generate a PDF with `gitbook pdf`.

See the [GitBook toolchain documentation][gitbook-toolchain] for more.

**Note:** If building in the lab fails with an `ENOENT: no such file or directory` error, try setting the output directory to a temporary folder:

```bash
gitbook serve . `mktemp -d`
```

[gh-pages]: https://dstelljes.github.io/container-project/
[gitbook]: https://github.com/GitbookIO/gitbook
[gitbook-toolchain]: http://toolchain.gitbook.com/
