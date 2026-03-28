# Running locally

One offs:

- `source "$(brew --prefix chruby)/share/chruby/chruby.sh" && chruby 3.4.9`
- If Ruby 3.4.9 is not installed yet: `ruby-install ruby 3.4.9`
- `bundle install`

Build and run:

- `bundle exec jekyll build`
- `bundle exec jekyll serve --livereload`

Then open: `http://127.0.0.1:4000/dev/`.
