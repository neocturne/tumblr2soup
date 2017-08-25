# tumblr2soup

*tumblr2soup* is a neat little script that will allow you to import posts from
Tumblr to Soup.io, without relying on Soup.io's builtin importer (which has been
broken for some time).

## Features

* Reads image posts from a Tumblr's RSS feed and posts on Soup.io
* Adds a source link to each post
* Properly supports image sets (each image will become a separate post, the
  description will be duplicated)
* Can be adjusted if needed

## Configuration

Copy the file ``config.rb.example`` to ``config.rb`` and add your data.

After a post is made, its GUID is stored in the file ``latest``. This allows the
importer to continue where it left off when running it again.

In case of failures, *tumblr2soup* will exit with an error message. ``latest``
will contain the last successful post; for posts with multiple images, this may
lead to duplicate images being added in the next run.

The ``latest`` file may be created manually. The GUID of a post has the form
``https://...tumblr.com/post/XXXXXXXX``, i.e. the post URL without anything
after the numeric post ID. The easiest way to find the GUID is to get it from
the Tumblr RSS feed.

Be wary of removing posts from Tumblr: removing a post while *tumblr2soup* is
running can cause posts to be skipped, and when the post that is stored in the
``latest`` file is removed, *tumblr2soup* will have no way to know where to stop
and re-import the whole Tumblr account.

## Known issues and missing features

* Can't post to Soup.io groups (should be easy to add, will need support in
  soup-client first)
* Doesn't retry on common failures
* Doesn't use the Soup API
  * The Soup API is not suitable for console tools (each user would have to
    apply for an API key; it seems only web applications are supported)
* At least on my Linux system, I couldn't get Ruby to access Soup.io's SSL
  certificate; I haven't been able to find the root cause of the issue yet.
  A very dirty hack to make it work is to disable certificate validation by
  adding ``OpenSSL::SSL::VERIFY_PEER = OpenSSL::SSL::VERIFY_NONE`` after
  ``require 'openssl'``. This is not recommended (better solutions are welcome).
