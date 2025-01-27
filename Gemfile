source 'https://rubygems.org'

## If you update the version here, also update it in .travis.yml, .ruby-version,
## and README.md. Then push your branch and make sure Travis supports that
## version.
ruby '3.2.2'

gem "asciidoctor", "~>2.0.20"
gem "rouge"

## If you add a new Gem below, run `bundle install` to install it.
group :development do
  gem "jekyll", "~> 4.3.2"
  gem "just-the-docs"
  gem 'jekyll-redirect-from'
  # Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
  # do not have a Java counterpart.
  #gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
end

group :jekyll_plugins do
  gem "asciidoctor-diagram"
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-asciidoc", "~> 3.0.0"
end

group :asciidoc_plugins do
  gem "asciidoctor-epub3"
  gem "asciidoctor-pdf"
end

group :testing do
  gem 'html-proofer'
  gem 'mdl'
  gem 'json-schema'
  gem 'toml'
end
