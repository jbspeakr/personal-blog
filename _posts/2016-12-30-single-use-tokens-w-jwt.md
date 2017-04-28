---
layout: post
title: Single-Use Tokens w/ JWT
permalink: howto-single-use-jwt/
description: Want to use JWT for password-reset or email activation? Turn app state into HMAC-keys to guarantee one-time use of JWTs! This is how it works ...
image: /assets/feature/jwt.png
category: appsec
---

[**JSON Web Tokens**](https://www.jbspeakr.cc/tag/jwt/) (JWTs) are the new and fancy de-facto standard in the web. JWTs are the tool of choice when it comes to authentication in an stateless environment. That has two direct implications:

<p class="subtitle">Self-contained JWTs can be used as one-time tokens. I'll show when this makes sense & how to implement it.</p>

- You should definitely go and get some [proper introduction](https://jwt.io/introduction/) on **how JSON Web Token work**. It's worth to know as JWTs are widely used for e.g. authentication against REST-APIs.
- Second, as JWTs are still fresh, hot and simply fancy, some people think they are some kind of holy Swiss army knife and can be used to solve every possible use-case... they are not!

## JWT Ain't Swiss Army

JSON Web Tokens are self-contained and stateless tokens. They are defined as an open standard in [RFC 7519](https://tools.ietf.org/html/rfc7519). Yet, JWT become truly powerful in combination with [RFC 7515](https://tools.ietf.org/html/rfc7515)  which describes JSON Web Signatures (JWS). Combined, the two standards create signed JWTs that can be trusted with little effort. Being self-contained, stateless and signed, JWTs allow you to leverage so-called **stateless authentication**.

But there are further possibilities to us JSON Web Tokens. One example I'd like to describe now is how to use JWTs as single-use tokens (also known as one-time tokens).

## Howto One-Time JWT

Let's talk about use-cases. Imagine you have a setup based on OAuth 2.0 that uses signed JWTs as bearer tokens for user-auth. Further imagine you want to provide [password-reset](https://www.troyhunt.com/everything-you-ever-wanted-to-know/) by email with confirmation-link included. For that confirmation-link we would then need to have a some kind of token (attached to the url). As the password-reset should work only once, the token is required to get invalided after usage. Hence, we would need a so-called single-use token.

One solution could be a token storage holding issued tokens and validity information. Every incoming password-reset request would then be checked against that central list. This stateful approach introduces a single point of truth. The token storage becomes the central bottleneck. Also, introducing yet another token mechanism makes our system more complex.

It would be great if another solution could leverage existing concepts. For example our stateless authentication system with its ability to create, sign and verify JWTs...

The solution for our problem is easy and straightforward as it is based on a simple trick. Although we can't alter issued JWTs, our backend is still the master of verification! We just need to look at JSON Web Token verification from another perspective.

<amp-img width="600" height="342" layout="responsive" src="/assets/images/one-time-jwt-diagram.jpg"></amp-img>

Using app-state as secret for the HMAC-based JWT signature helps in this use-case. Signing with the users current password hash guarantees single-usage of every issued token. This is because the password hash always changes after successful password-reset. There is no way the same token can pass verification twice. The signature check would always fail. The JWTs we issue become single-use tokens.

## TL;DR

So let's sum up our findings on how to implement single-use tokens based on JWT.

- First, there is no need to setup some kind of token-registry storage. This would counter the idea of stateless, self-contained tokens anyway.
- Instead, compose signature secrets based on values that change after each token usage. In other words: **Turn app state into HMAC-keys to guarantee one-time use of JWTs!**

In theory, this also works with use-cases besides password-reset tokens e.g. email activation, account confirmation etc. However, my thoughts took shape while solving this specific issue. If you know other approaches to achieve single-use JWTs do not hesitate to write a comment. I also appreciate feedback and further discussion. Thanks!
