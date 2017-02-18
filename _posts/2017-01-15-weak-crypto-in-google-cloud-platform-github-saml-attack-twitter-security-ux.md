---
layout: post
title: Weak Crypto in Google Cloud Platform, Github SAML Attack & Twitter Security UX
permalink: weak-google-crypto-github-saml/
description:
image: /assets/images/twitter-security-ux.jpg
---

Finally, I managed to come up with a name for my regular reading tips series which will feature both, latest info around recent events & incidents (especially when it comes to identity and security topics) as well as long running articles I strongly advice to read... it's simply called **Readme**.

The first issue of my Readme series features not just the latest *Google Infrastructure Security Design Overview* but also the most recently fixed SAML authentication bypass in GitHub Enterprise. As a small bonus on top, I'd like to share a nice UX security analysis regarding Twitters "someone is logging in to your account" e-mail, I recently stumbled upon. But first things first...

## Weak Crypto in Google Cloud Platform?!
Google just released the latest version of its [*Google Infrastructure Security Design Overview*](https://cloud.google.com/security/security-design/) that describes how security is designed into Google’s technical infrastructure. It's a quite interesting paper for everyone, relying on Google Services but also for people who want to know how current industry standards look like. In addition to operational security and hardware infrastructure, it also considers authentication and login abuse as well as end user data access and inter-service access.

I am not quite done reading it, but one interesting catch so far is that Google Cloud Platform products seem to be heavily based on the *"common cryptographic library, Keyczar"*, which actually is made by Google and states [on its project page](https://github.com/google/keyczar)...

> “KeyCzar has some known security issues which may influence your decision to use it.”

One of the known issues is the usage of 1024 bit DSA keys with SHA1... nothing more to add, I believe.

## GitHub SAML Vulnerability
January 12th, a critical security patch was rolled out for Github Enterprise. In accordance to the [official release notes](https://enterprise.github.com/releases/2.8.6/notes), it fixes a major issue that allowed the bypass SAML authentication which was found and reported by [Ioannis Kakavas](https://twitter.com/ilektrojohn/status/819919288215760897). Github strongly advices to update asap!

Critical security issues in SAML implementations are not new, as German security researchers already showed back in 2012: [On Breaking SAML - Be Whoever You Want to Be](https://www.usenix.org/conference/usenixsecurity12/technical-sessions/presentation/somorovsky).

## Bad Security UX at Twitter
Being open and transparent towards your endusers when it comes to (possible) security issues can be a good thing to do. But you can also do a lot wrong about it - e.g. when your phishing or login fraud countermeasures turn against you (and your customers).

<amp-img width="600" height="417" layout="responsive" src="/assets/images/twitter-security-ux.jpg"></amp-img>

One of the examples, that actually illustrate how not to communicate a possible account compromise is Twitters "someone is logging in to your account" e-mail that can (and should) be optimized/ fixed as [pwnallthethings described on Twitter](https://twitter.com/pwnallthethings/status/817923705993043968)... well done!

That's it for now, so have fun reading and stay secure!
