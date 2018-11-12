---
layout: post
title: "Brute-Force Defense: Preventing Customer Account Hacking"
permalink: bruteforce-login-attack-defense/
description: "Brute-force attacks are the most common and wide-spread security threats not just to eCommerce but all restricted areas on the web. Let's see how to defend..."
image: assets/images/brute-force-attack.png
category: appsec
---

**The very diverse nature of brute-force attacks and their technical foundation
make them difficult to stop completely. But with careful design and multiple
countermeasures, exposure to these attacks can be limited. The following text
highlights common attack schemes and possible counter-measures...**

To gain access to restricted areas on the web (like customer accounts), modern criminals, test engineers
and security researchers have a wide variety of different tools and attacks at their command.
One of the most common, easy and wide-spread security threats regarding credential
gathering are brute-force attacks.


## Identify Brute-Force Attacks

The first powerful weapon against attacks of any kind is to know that your
application is vulnerable and that you are (constantly) under attack. Monitoring
authentication processes is a duty, everybody involved should carry out with
patience and thoroughness. It's not just your companies reputation that is
at risk, but the digital identities and user experience of your customers or co-workers.

Being able to answer these and similar questions is a first step for creating
self-awareness: Can you explain all the unusual spikes in your successful login
requests graph? Do you know how many logins and password changes you should expect
to happen? Can you really trust your authentication challenges? And do you enforce
authentication best-practices or simply dump the responsibility on the users/ customers side?

<figure>
  <amp-img width="600" height="169" layout="responsive" src="/assets/images/brute-force-attack.png"></amp-img>
  <caption>Ongoing Brute-Force Attack(s)</caption>
</figure>

To recognize and limit exposure to brute-force attacks, it's important to understand their true nature.
With password-guessing, reverse brute-force and public credential leaks, at least three different classes of explorative credential and access gathering can be distinguished. Together they represent the foundation of a noisy baseline of ongoing attacks for probably every internet-facing application.

## Password-Guessing
Most common attacks try to leverage weak passwords. They do this by following simple trial-and-error methods like simply guessing random passwords for a known user identifier. More sophisticated approaches make use of publicly available knowledge like the [most common passwords](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords) or pseudo-scientific data on how average people compose their secrets.

As these so-called [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack) (hopefully) result in a non-expected high number of failing login attempts per user ID (or login name, e-mail address, ...), exposure can be reduced by introducing CAPTCHAs or soft locks (also known as request or rate limits). Both counter-measures limit impacts of automated attacks by adding anti-machine challenges or at least decrease attackers return of investment by increasing invested time.

## Reverse Brute-Force
Approaching credential gathering from a slightly different angle reverse brute-force attacks try to leverage knowledge about popular passphrases even more. Unlike simple password guessing, they actually try to find a user identifier for a given password. By testing commonly used passwords against multiple usernames, attackers bet the odd of e.g. finding the [4% users](http://time.com/4639791/worst-passwords-2016/) that use "123456" as their password.

What makes reverse brute-force attacks really evil is that it's nearly impossible to defend against them. Although you will be able to witness an increased number of failed logins when under attack, you won't be able to (soft) block certain accounts. In a best case scenario, all you could do is block, limit or delay requests from specific IPs – but facing serious attacks, that's not going to help you for long...

## Drip Attacks

That feeling of practical helplessness becomes even more depressing when you imagine attackers who are not interested in quick-wins but operate with patience. Both, simple password-guessing and reverse brute-force attacks can be executed as so-called [drip attacks](https://perishablepress.com/brute-force-login-drip-attack/). With one drip at a time, these slowly performed attacks hide in the usual baseline of failing customer logins and are (if at all) only hard to notice. Hence, they are also almost impossible to fight. The only thing that probably could help is global intelligence and a regularly updated list of attacking IPs that serves as input for proactive blocking – but this again would lead to other challenges.

## Brute-Force Counter Measures
Due to the very diverse nature of brute-force attacks it is very difficult to defend your systems and your customers data. There is no silver bullet that helps you prevent from customer account hacking and I doubt that anyone will ever prevent password-guessing and dripping attacks from happening.

Effective defense however starts with awareness on both sides, the login provider and it's consumer. Furthermore, every login-system should be build following security by design approaches and incorporate multiple of the following counter-measures:

* (Almost) unpredictable login response behaviour (different status codes, different pages, ...)
* Whitelist trusted IP addresses
* Multi-factor authentication (MFA)
* Captcha or similar methods
* Rate-limiting (execution delay after a failed login attempt)
* Block IPs after too many failed login attempt
* Blacklist known malicious IPs

Of course this list is neither ordered nor exhaustive. If you know further approaches to defend from brute-force login attacks do not hesitate to drop me message [via Twitter](https://www.twitter.com/jbspeakr). I also appreciate feedback and further discussion. Thanks!
