---
type: posts
title: Automatically save all email attachments in Apple Mail
date: 2019-08-06
categories: applescript
tags: automation
description: Automatically save every attachment from emails received in Apple Mail to Dropbox using Applescript
permalink: /automation/autosave-email-attachments
---
Automatically save every attachment from emails received in Apple Mail to Dropbox using Applescript.
<!--more-->

Until recently, I used an [IFTTT][ifttt] rule to save all attachments from
emails received by my Gmail account to Dropbox. Unfortunately, Google changed the Gmail
API, so [all Gmail triggers were removed][ifttt-gmail] from IFTTT. This meant that my
rule to save attachments stopped working.

I briefly considered changing email providers, but decided instead to see if I
could automate the saving of email attachments myself. After some Googling,
I found that in 2013 someone had managed to create [an Apple Mail rule which saved all email attachments][original].
Of course, the [Applescript attached][original] in that post didn't work right out
of the box on `macOS 10.14.5`, so I needed to make a few edits ([my version][myscript] is linked
at the bottom of this post). Using a local `Mail.app` rule instead of IFTTT has
the disadvantage that this automation only works when my Mac is turned on, but
it's better than the alternative of having no automation at all.

Apart from setting `~/Dropbox/mail` as the destination folder, there's some semantic
differences as to how to access the Mail messages and the sender of each message.
As well, use of shell commands to create directories has been removed in favour of a
pure Applescript implementation which uses `tell application "Finder"`.

For each email that comes in, if the email has at least one attachment, the script
will create the directory `~/Dropbox/mail/$SENDER/` if it doesn't exist already.
Here `$SENDER` is set to be the exact address of the sender. The script
then saves every attachment to `~/Dropbox/mail/$SENDER/`.

In order to get this script to run on every email, we need to create a rule
in Mail.app:

<img width="300" src="/images/posts/mail_rule.png" alt="Mail rule">

I don't really want to save attachments from every email, so I use a whitelist,
but this rule can be easily tweaked to run on every single email you receive.

In order to run Applescripts in `Mail.app` rules, we need to save the Applescript
in the application scripts folder. I use a hardlink from my scripts repo so I
don't have to worry about remembering to keep the one hidden in ~/Library updated:

`$ ln attachment-saver.applescript ~/Library/Application Scripts/com.apple.mail/attachments`

Here's the script which works on `macOS 10.14.5`, if you're interested:
{% gist 7e5f4afbba6f09199dd4677cc57dc70d %}

Cataloging my email like this is good for injesting into folders that have
[Hazel][hazel] rules run on them, but that's a story for another time.

[ifttt]: https://ifttt.com/
[ifttt-gmail]: https://help.ifttt.com/hc/en-us/articles/360020249393-Important-update-about-the-Gmail-service
[original]: http://www.markosx.com/thecocoaquest/automatically-save-attachments-in-mail-app/
[myscript]: https://gist.github.com/patrickleweryharris/7e5f4afbba6f09199dd4677cc57dc70d
[hazel]: https://www.noodlesoft.com/
