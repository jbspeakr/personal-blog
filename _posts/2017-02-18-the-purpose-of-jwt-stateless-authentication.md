---
layout: post
title: 'The Purpose of JWT: Stateless Authentication'
permalink: purpose-jwt-stateless-authentication/
description: JSON Web Token allow to establish stateless authentication. I'll explain why this is important and what's the fundamental difference to stateful auth.
image: assets/images/stateful-vs-stateless.png
category: appsec
---

**JSON Web Tokens or just JWTs (pron. [ˈdʒɒts])** are the new fancy kids around the block when it comes to transporting proofs of identity within an untrusted environment like the web. In this article, I will describe the true purpose of JWTs. I will compare classical, stateful authentication with modern, stateless authentication. And I will explain why it is important to understand the fundamental difference of both approaches.

<figure>
  <amp-img width="600" height="321" layout="responsive" src="/assets/feature/jwt.png"></amp-img>
  <caption>A JSON Web Token</caption>
</figure>

While there are many good articles available that describe specific aspects, [best practises](https://dev.to/neilmadden/7-best-practices-for-json-web-tokens) or single use-cases of JWTs, the bigger picture is often missing. The actual problem the JWT specs try to solve is just not part of most discussions. With JWTs however gaining in popularity, that missing knowledge of the fundamental ideas of JSON Web Token leads to serious questions like,

- [How to invalidate a JWT](https://stackoverflow.com/questions/21871029/logout-invalidate-a-jwt),
- [How to prolongate a JWTs expiration date](https://stackoverflow.com/questions/26739167/jwt-json-web-token-automatic-prolongation-of-expiration) or
- [Why should I use JWT, not simple hashed token](https://stackoverflow.com/questions/41865108/why-should-i-use-jwt-not-simple-hashed-token).

This article is not about symptoms, but the purpose of JWT which actually is: **Getting rid of stateful authentication!**

## Stateful Authentication

In the old days of the web, authentication was a pure stateful affair. With an centralized overlord entity being responsible for tokens, the world was fairly simple:

- Tokens are issued and stored in a single service for future checking and revocation,
- Clients and resource servers know a single point of truth for token verification and information gathering.

This worked rather well in a world of integrated systems (some might call them legacy app, mothership or simply [Jimmy](https://tech.zalando.com/blog/from-jimmy-to-microservices-rebuilding-zalandos-fashion-store/)), when servers rendered frontends and dependencies existed on e.g. package-level and not between independently deployed applications.  

In a world where applications are composed by a flock of autonomous microservices however, this stateful authentication approach comes with a couple of serious drawbacks:

- Basically no service can operate without having a synchronous dependency towards the central token store,
- The token overlord becomes an infrastructural bottleneck and single point of failure.

Eventually, both facts oppose the fundamental ideas of [microservice architectures](https://www.jbspeakr.cc/microservice-evolution/). Stateful authentication introduces not just another dependency for all your single-purpose services (network latency!) but also makes them heavily rely on it. Without the token overlord being available (even for just a couple of seconds) everything is doomed. This is why a different approach is required: **Stateless Authentication!**

<figure>
  <amp-img width="600" height="356" layout="responsive" src="/assets/images/stateful-vs-stateless.png"></amp-img>
  <caption>The World becomes Stateless - Google Trends</caption>
</figure>

## Stateless Authentication

Stateless authentication describes a system/ process, that enables its components to decentrally verify and introspect tokens. This ability to delegate token verification allows to (partly) get rid of the direct coupling to a central token overlord and in that way enables state transfer for authentication. Having worked in stateless auth environments for several years, the benefits in my eyes are clearly:

- Less latency through local, decentralized token verification,
- Custom authorization fallbacks due to local token interpretation,
- Increased resilience by removed network overhead.

Also, stateless authentication is able to absolve from the need to keep track of issued tokens and for that reason removes state (and hence reduces storage) dependencies from your system.

The antiquated, heavy-weighted token overlord converges to yet another microservice being mainly responsible for issuing tokens. All of this comes in handy especially when your world mainly consists of single-page applications or mobile clients and services that primarily communicate using RESTful APIs.

> “Using a JWT as a bearer for authorization, you can statelessly verify if the user is authenticated by simply checking if the expiration in the payload hasn't expired and if the signature is valid.”
> — <cite><a href="http://jonatan.nilsson.is/stateless-tokens-with-jwt/" title="Stateless tokens with JWT">Jonatan Nilsson</a></cite>

One popular way to achieve stateless authentication is defined in [RFC 7523](https://tools.ietf.org/html/rfc7523) and leverages the OAuth 2.0 Authorization Framework ([RFC 6749](https://tools.ietf.org/html/rfc6749)) by combining it with server-signed JSON Web Tokens ([RFC 7519](https://tools.ietf.org/html/rfc7519), [RFC 7515](https://tools.ietf.org/html/rfc7515)). Instead of storing the token-to-principal relationship in a stateful manner, signed JWTs allow decentralized clients to securely store and validate access tokens without calling a central system for every request.

With tokens not being opaque but locally introspectable, clients could also retrieve addition information (if present) about the corresponding identity directly from the token without the need of calling another remote API.

## Stateful vs. Stateless

Nowadays in a web that is mainly characterized by a wide-spread transition from monolithic legacy apps to decoupled microservices, a centralized token overlord service can be described as an additional burden. The purpose of JWT is to obviate the need for such a centralistic approach.

However there again is no silver bullet and JWTs ain’t Swiss army knifes. Also stateful auth has its righteous place. If you really need a central authentication system (e.g. to fulfill restrictive auditing requirements) or if you simply don't trust people [or libraries](https://www.chosenplaintext.ca/2015/03/31/jwt-algorithm-confusion.html) to correctly verify your JWTs, a stateful overlord approach is still the way to go and there is nothing wrong about it.

Anyway, you probably shouldn't mix both approaches. To shortly answer the questions above:

- There is no way of invalidating a JWT, expect if you just use it as yet another random string within a stateful authenticating system,
- There is no way of altering an issued JWT, so prolongating its expiration date is again not possible.
- You could use JWTs if they really help you solving your issues. You don't have to use them. You can also keep your opaque tokens.

If you have further comments regarding the purpose of JWT or if you think I missed something important, do not hesitate to drop me message [via Twitter](https://www.twitter.com/jbspeakr). I also appreciate feedback and further discussion. Thanks!
