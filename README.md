# The github-pages gemPermalink

Our friends at GitHub have provided the github-pages gem which is used to manage Jekyll and its dependencies on GitHub Pages. Using it in your projects means that when you deploy your site to GitHub Pages, you will not be caught by unexpected differences between various versions of the gems.

Note that GitHub Pages runs in safe mode and only allows a set of whitelisted plugins.

To use the currently-deployed version of the gem in your project, add the following to your Gemfile:
~~~
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
~~~
Be sure to run: **bundle update** often.



# Forty - Jekyll Theme

A Jekyll version of the "Forty" theme by [HTML5 UP](https://html5up.net/).  

Forty by HTML5 UP
html5up.net | @ajlkn
Free for personal and commercial use under the CCA 3.0 license (html5up.net/license)
