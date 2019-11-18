## [Click here to my homepage](https://xinii.github.io/)

## Tips for run in local:

* Add the configure below to `Gemfile`, then run `bundle install`.

```Gemfile
gem 'jekyll-coffeescript'
gem 'jekyll-default-layout'
gem 'jekyll-gist'
gem 'jekyll-github-metadata'
gem 'jekyll-optional-front-matter'
gem 'jekyll-paginate'
gem 'jekyll-readme-index'
gem 'jekyll-titles-from-headings'
gem 'jekyll-relative-links'
```

* When finished install, add the configure below to `_config.yml` and uncomment `remote_theme`.
> May not need, you can try the next step first, if it can not run well, do this step.

```yml
plugins:

  - jekyll-coffeescript
  - jekyll-default-layout
  - jekyll-gist
  - jekyll-github-metadata
  - jekyll-optional-front-matter
  - jekyll-paginate
  - jekyll-readme-index
  - jekyll-titles-from-headings
  - jekyll-relative-links
```

* Run `jekyll serve` or `bundle exec jekyll serve` or `bundle exec jekyll serve --port 80`.
