---
layout: post
title: How to fix Jekyll build warnings
categories: [how-to, jekyll]
excerpt: You are using Jekyll to build your website, and you are getting a few build warnings from Jekyll like these,
---

## Problem:

You are using Jekyll to build your website, and you are getting a few warnings like these when you run the command,
```text
jekyll serve
```
```text
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils/version.rb:4: warning: already initialized constant FileUtils::VERSION
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:105: warning: previous definition of VERSION was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils.rb:1267: warning: already initialized constant FileUtils::Entry_::S_IF_DOOR
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:1284: warning: previous definition of S_IF_DOOR was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils.rb:1540: warning: already initialized constant FileUtils::Entry_::DIRECTORY_TERM
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:1568: warning: previous definition of DIRECTORY_TERM was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils.rb:1595: warning: already initialized constant FileUtils::OPT_TABLE
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:1626: warning: previous definition of OPT_TABLE was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils.rb:1649: warning: already initialized constant FileUtils::LOW_METHODS
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:1685: warning: previous definition of LOW_METHODS was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/fileutils.rb:1656: warning: already initialized constant FileUtils::METHODS
/Library/Ruby/Gems/2.6.0/gems/fileutils-1.4.1/lib/fileutils.rb:1692: warning: previous definition of METHODS was here
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/universal-darwin19/strscan.bundle: warning: already initialized constant StringScanner::Version
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/universal-darwin19/strscan.bundle: warning: already initialized constant StringScanner::Id
```
Your error output will most likely be a bit different from the above example but the important error parts to note down are,
```text
warning: already initialized constant...
warning: previous definition was here...
```
Your site builds and deploys correctly despite these errors but you want to get rid of these errors, don't you? yes, you do.

## Solution:

First remove the file <inline-code>Gemfile.lock</inline-code> from the root of your site.  
Next run this command in terminal from the root of your site,
```text
bundle update
```
This should fix those bugging errors.  
Whenever in the future you want to build your site and you have a <inline-code>Gemfile</inline-code> in your site's root directory you always must build your site with this command,
```text
bundle exec jekyll serve
```

Cheers!!!  
