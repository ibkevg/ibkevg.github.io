# The github-pages gemPermalink

--- Begin KDG NOTES

I used this webpage (Jan/2025) to setup a Ruby env that is not the one provided by MacOS:
https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/


Then I did:
https://www.moncefbelyamani.com/how-to-install-jekyll-on-a-mac-the-easy-way/#spend-an-hour-or-more-installing-jekyll-on-mac-manually

I ran into an issue doing: gem install jekyll:
https://github.com/eventmachine/eventmachine/issues/990

Do this, if it says "false" you have a problem and need to sort out the xcode command line tools
ruby -rrbconfig -e 'puts RbConfig::CONFIG["CXX"]'

It should show clang++



There is also this youtube video that people seem to like but I didn't use it:
https://www.youtube.com/watch?v=UKB9ylw0G4U

--- End KDG NOTES



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
