source 'https://rubygems.org'


# Ensure we always use the current version of github pages that is used
# by actual github.
require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']