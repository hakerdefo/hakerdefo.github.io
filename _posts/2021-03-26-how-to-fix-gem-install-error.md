---
layout: post
title: How to fix gem install error
categories: [how-to, gem]
slug: fix-gem-install-error
excerpt: You are trying to install a Ruby gem but installation is failing with an error "Failed to build gem native extension". What is causing this error and what is the solution?
---

## Problem:

You are trying to install a Ruby gem but installation is failing with an error something like this,
```text
Failed to build gem native extension
```
Most likely cause of these errors is missing build dependencies. Let's dig into a couple of solutions.

## Solution:

First make sure you have these minimum prerequisites installed on your system,
```text
sudo apt-get install ruby-full build-essential zlib1g-dev
```
Next I'll give you an example on how you can search and install missing build dependencies for a particular case.  
Let's say I'm' trying to install the gem <inline-code>sass</inline-code> on my system and installation is failing with errors,
```text
gem install sass
Building native extensions.  This could take a while...
ERROR:  Error installing sass:
    ERROR: Failed to build gem native extension.
/usr/bin/ruby2.2 -r ./siteconf20180217-38265-1l6kefu.rb extconf.rb
checking for ffi.h... no
checking for ffi.h in /usr/local/include,/usr/include/ffi... no
checking for shlwapi.h... no
checking for rb_thread_blocking_region()... no
checking for rb_thread_call_with_gvl()... yes
checking for rb_thread_call_without_gvl()... yes
creating extconf.h
creating Makefile

make "DESTDIR=" clean

make "DESTDIR="
Running autoreconf for libffi
/var/lib/gems/2.2.0/gems/ffi-1.9.21/ext/ffi_c/libffi/autogen.sh: 2: exec: autoreconf: not found
make: *** ["/var/lib/gems/2.2.0/gems/ffi-1.9.21/ext/ffi_c/libffi-x86_64-linux-gnu"/.libs/libffi_convenience.a] Error 127

make failed, exit code 2
```
In the above output what you need to look for is the lines ending with a <inline-code>no</inline-code> and containing file names that end with a <inline-code>.h</inline-code>.
We can extract three lines that meet our criteria,
```text
checking for ffi.h... no
checking for ffi.h in /usr/local/include,/usr/include/ffi... no
checking for shlwapi.h... no
```
First two lines have the same header file <inline-code>ffi.h</inline-code> while the third line mention the header file <inline-code>shlwapi.h</inline-code>.
So the build is failing because of these two missing header files. We need to install packages that provide these header files.  
How do we find these packages? Well, the solution mentioned here is for Debian but can easily be adopted for other distributions.  
Open the Debian package content search page,  

[Debian package content search](https://www.debian.org/distrib/packages#search_contents){:target="_blank"}  

In the **Keyword** field enter <inline-code>ffi.h</inline-code>. Under the **Display** section select **packages that contain files named like this**. Finally select Debian **Distribution**, **Architecture** and hit the **Search** button.  
From the search result page we can see that <inline-code>libffi-dev</inline-code> is the package that provides <inline-code>ffi.h</inline-code> header file.
We repeat the above search procedure for <inline-code>shlwapi.h</inline-code> and find that <inline-code>mingw-w64-i686-dev</inline-code> provides that particular header file.
Now all we need to do is install these packages,
```text
sudo apt-get install libffi-dev mingw-w64-i686-dev
```
Now <inline-code>sass</inline-code> gem can be installed without any build errors.  
You can adopt this approach to identify missing dependencies and find the relevant packages providing those dependencies.  

Cheers!!!  
