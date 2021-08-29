---
type: posts
title: Automatically export .docx documents to PDF using Pages
date: 2019-08-19
categories: applescript
tags: automation
description: Automatically export .docx documents to PDF using Pages
permalink: /automation/docx-to-pdf/
---
Automatically export .docx documents to PDF using Pages
<!--more-->

I often receive emails with attachments in .docx format. The Pages app
on Mac is capable of editing and saving these documents, but if I don't need
to edit a document I prefer to save these documents as PDFs, which
makes it easier to open them anywhere (mobile, different computers, etc...).

If you get a lot of emails with .docx attahcments, this can become time consuming
and repetitive. I've designed the following AppleScript to automatically convert
.docx documents to PDF using Pages:

{% gist 32caecd150a5d69cc379540709c2e8dc %}

I use this script in conjunction with a [Hazel][hazel] rule on my 'inbox' folders (organized by email of sender), with the documents being saved
to those folders by another [AppleScript which runs in an mail.app rule][autosave-attachments].

The Hazel rule looks like this:
![Docx converter](/images/posts/docx_converter.png)

The 'embedded script' in the AppleScript is the [gist attached above][gist].



[hazel]: https://www.noodlesoft.com/
[autosave-attachments]: http://plh.io/automation/autosave-email-attachments
[gist]: https://gist.github.com/patrickleweryharris/32caecd150a5d69cc379540709c2e8dc
