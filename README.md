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

You will need a recent version of Ruby to run *tumblr2soup*, and the tool
*bundler*. After downloading the *tumblr2soup* repository, simply run
``bundle install`` to install all dependencies.

Copy the file ``config.yml.example`` to ``config.yml`` and add your data.

After a post is made, its ID is stored in the file ``latest``. This allows the
importer to continue where it left off when running it again.

In case of failures, *tumblr2soup* will exit with an error message. ``latest``
will contain the last successful post; for posts with multiple images, this may
lead to duplicate images being added in the next run.

The ``latest`` file may be created manually. The ID of a post has the form
``XXXXXXXX`` for a post URL ``https://...tumblr.com/post/XXXXXXXX/...``.

Be wary of removing posts from Tumblr: removing a post while *tumblr2soup* is
running can cause posts to be skipped, and when the post that is stored in the
``latest`` file is removed, *tumblr2soup* will have no way to know where to stop
and re-import the whole Tumblr account.

## Known issues and missing features

* Can't post to Soup.io groups (should be easy to add, will need support in
  soup-client first)
* Infinite retry on failures (should be limited and should distinguish between
  failure types)
* Doesn't use the Soup API
