---
type: posts
title: Delete All Saved Reddit Links
date: 2019-07-28
tags: automation
categories: python
description: Delete all saved links from your Reddit account automatically with Python and PRAW
permalink: /automation/delete-all-saved-reddit-links
---
Delete all saved links from your Reddit account automatically with Python and PRAW.
<!--more-->

If you're like me, then you have a lot of saved Reddit posts. This can get
taxing after a while, so sometimes you just need to clean house and get rid
of them all. There's not an easy way to do this directly from
Reddit. There are [some websites][reddit-manager] which can interface with
your Reddit account for managing your posts and saved content, but that's
just another third party service you're giving your info to.

Thankfully, Reddit provides a pretty good [API][reddit-api], and the [PRAW][praw]
("Python Reddit API Wrapper") module provides a great way to create scripts
to manipulate your account.

When using PRAW, the first thing you're going to need to do is register
an API application with Reddit. This will give you a `Client ID` and `Client Secret`
which need to be given to PRAW when you intialize. Instructions for this can
be found in the [PRAW documentation][praw-doc]. Once you have this info, you
can use the script below to delete all your saved posts.

The script can be used like so:

`$ python delete_saved.py CLIENT_ID CLIENT_SECRET PASSWORD USERNAME`

The script will get up to 1000 of your saved posts, and delete them from your Reddit
account. If you have more than 1000 saved posts, you can run the script multiple times.


{% gist 4374752c0051e1afe73470d6b002ec87 %}

This script is adapted from an older version I found on Github a while back, but I
can't seem to find the link.

[reddit-manager]: https://redditmanager.com/
[reddit-api]: https://www.reddit.com/dev/api/
[praw]: https://praw.readthedocs.io/en/latest/
[praw-doc]: https://praw.readthedocs.io/en/latest/getting_started/authentication.html
