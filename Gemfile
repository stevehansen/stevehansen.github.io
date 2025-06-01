source "https://rubygems.org"

# Specify Jekyll version compatible with GitHub Pages
# This will also pull in associated gems like kramdown, rouge, etc.
gem "jekyll", "~> 3.9.0"

# GitHub Pages specific gems
# Using the 'github-pages' gem helps ensure compatibility
# It includes jekyll, jemoji, jekyll-sitemap, jekyll-redirect-from, etc.
group :jekyll_plugins do
  gem "github-pages", "~> 220", :require => false
  gem "faraday-retry"
  # "~> 220" corresponds to a recent version that supports Jekyll 3.9.x
  # If specific versions of plugins are needed, they can be listed here too,
  # but github-pages gem usually handles this well.
end

# Add other plugins if they are not part of github-pages group
# For example, if 'jekyll-feed' was used and not included by 'github-pages'
# gem "jekyll-feed", "~> 0.12"
