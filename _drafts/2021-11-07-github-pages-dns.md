---
type: posts
title: I Got Pwned By DNS
date: 2021-11-07
categories: security
description: DNS Hijacking is apparently a feature of Github Pages - but there’s a way out
---
I was looking over my Google Search console today, and I saw something strange for my history blog [napoleonvswellington.org][nnn]

A subdomain “uquailahzu.napoleonvswellington.org” was active, with a bunch of pages under it. It's Russian language I think, so unsure of what exactly it was. But there were some mentions of “iPhone 5s” in the URLs, so I assume it’s spam.

![Screenshot of the malacious URLs that showed up in Google Search Console](/images/posts/nnn-hacked.jpeg)

In a panic, I checked my DNS and registry, but no mention of the subdomain was found. So my accounts at least have not been compromised. 

Then I noticed that my DNS A records had a wildcard in it:

| Type | Name | Content |
|------|------|---------|
|A | *| 123.456.789 |
|A |www| 123.456.789|


I set this site up years ago, so I wondered if this was the proper configuration… so I checked [Github’s support article][github-custom-domain-setup], and sure enough I see this big warning:

![Warning from Github about using *](/images/posts/github-warning.jpeg)

Well… oops. Changing my DNS records to be a non-wildcard, the malicious spam subdomain quickly disappears and can no longer be reached (Thanks Cloudflare for the fast updates!):

| Type | Name | Content |
|------|------|---------|
|A | @ | 123.456.789 |
|A |www| 123.456.789|

Problem solved! But why did this happen?

Turns out, I’m not the first person to see this issue. 

There’s a proof of concept from deepwn available [here][deepwn], showing that many, many Github Pages sites are at risk for this issue. Jehy on Medium has a [great write up for a similar issue he faced][medium]. 

Bottom line: Never ever ever use wildcard DNS records for a site that runs on Github Pages. Domain hijacking is a feature!

However… there is some redemption for GitHub here. They have a tool for verifying a domain, which appears to have [launched only a week ago on November 1st][news]. Github has a nice how to guide [here][verify], so I won’t go into details. But it should prevent this kind of issue from ever happening again, since “[w]hen you verify your custom domain for your user account or organization, only repositories owned by your user account or organization may be used to publish a GitHub Pages site to the verified custom domain or the domain's immediate subdomains.”

So, in short:

- Never add wildcard (\*) A records to the DNS records for a Github Pages site
- Verify your domain(s) with Github just in case.

Some additional reading on \* vs. @ records can be found [here][dns]. They are
often used interchangeably but they are not the same (see above!).

P.S. It looks like the feature that the [deepwn team recommended][deepwn] is
actually what Github implemented for their verification feature. Good on Github
for following up - even if they determined the bug found to not be elgible for
the bug bounty

[nnn]: https://napoleonvswellington.org
[github-custom-domain-setup]: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain
[deepwn]: https://github.com/deepwn/GitPageHijack
[medium]: https://medium.com/@jehy/hijacking-domain-using-github-pages-41c80ac57523
[news]:  https://github.blog/changelog/2021-11-01-domain-verification-for-github-pages/
[verify]: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages
[dns]: https://www.apexdigital.co.nz/blog/wildcard-versus-exact-match-dns-records/

