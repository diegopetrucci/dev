# Repository Guidelines

## Project Structure & Module Organization
- `_posts/` holds blog posts. Filenames must be date-prefixed: `YYYY-MM-DD-kebab-case-title.markdown`.
- `assets/` stores images and other static files referenced by posts and pages.
- `index.markdown` and `about.markdown` are top-level pages with front matter.
- `_config.yml` contains site configuration; `Gemfile`/`Gemfile.lock` define Ruby/Jekyll dependencies.
- `_site/` is the generated output from Jekyll builds; avoid manual edits here.

## Build, Test, and Development Commands
- Ruby 3.4.9 is required. With `chruby`, install it via `ruby-install ruby 3.4.9` if needed.
- The documented workflow assumes Homebrew, `chruby`, and `ruby-install` are already available.
- Load `chruby` in your shell before running commands, for example `source "$(brew --prefix chruby)/share/chruby/chruby.sh" && chruby 3.4.9`. If you also load `auto.sh`, the repo’s `.ruby-version` will auto-select Ruby 3.4.9.
- `bundle check || bundle install` installs Ruby gems only when needed.
- `bundle exec jekyll build` produces the static site in `_site/`.
- `bundle exec jekyll serve --livereload` runs the local dev server and rebuilds on changes.
- The site `baseurl` is `/dev`, so open `http://127.0.0.1:4000/dev/`, not `http://127.0.0.1:4000/`.
- Current builds emit Sass deprecation warnings from the remote theme; treat a zero exit code as a successful build.
- `bundle exec jekyll clean` (optional) clears caches if builds behave oddly.
- Deployment: the default branch is `gh-pages`, and pushes to `gh-pages` trigger the GitHub Pages workflow in `.github/workflows/pages.yml`.

## Coding Style & Naming Conventions
- Content is Markdown with YAML front matter. Keep front matter minimal and consistent:
  ```yaml
  ---
  layout: single
  title: My Post Title
  ---
  ```
- Use two-space indentation in YAML; no tabs.
- Use kebab-case for filenames and asset names (e.g., `self-improving-agents-header.png`).
- Prefer short paragraphs and clear headings for posts; keep titles descriptive.

## Testing Guidelines
- There are no automated tests. Validate changes by running `bundle exec jekyll build` or `bundle exec jekyll serve`.
- For content changes, spot-check rendered pages and verify image/link paths.

## Commit & Pull Request Guidelines
- Commit messages in history are short and imperative (e.g., “add a header image”). Keep them concise and specific.
- PRs should include a brief summary, list of affected posts/pages, and screenshots for visual/layout changes. Link related issues when applicable.

## Content & Configuration Tips
- Avoid committing secrets or private data in `_config.yml` or posts.
- When adding new posts, confirm the date in the filename matches the intended publish date.
