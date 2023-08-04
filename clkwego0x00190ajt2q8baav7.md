---
title: "How PayPal Almost Lost Their Database."
seoDescription: "The key splitting code was developed on Linux, but the production system ran Solaris. Due to an outdated difference between the platforms."
datePublished: Fri Aug 04 2023 09:45:02 GMT+0000 (Coordinated Universal Time)
cuid: clkwego0x00190ajt2q8baav7
slug: how-paypal-almost-lost-their-database
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691142156765/9689155d-80fb-43f7-b76c-e8a3b6c3b30b.jpeg
tags: database, paypal, cryptography, incident

---

It was just another late night at PayPal headquarters. Engineers were working to improve the security of the payment processing system by implementing Shamir's Secret Sharing to protect the master encryption key. The idea was to split the key into shards and require multiple passphrases to reconstruct it, preventing any single person from accessing the key.

Everything seemed to be going smoothly. The shards were generated, passphrases were chosen, and the new encrypted database was deployed. But when it came time to restore the master key, disaster struck - the shards would not reconstruct!

After some debugging, the culprit was found. The key splitting code was developed on Linux, but the production system ran Solaris. Due to an outdated difference between the platforms, passphrases over 8 characters were truncated on Solaris. All the carefully chosen passphrases were reduced to 8 characters, rendering the shards useless.

Panic set in as the engineers realized the master key was lost with no backups. The only shard that worked was set up with the insecure passphrase "a$$word". After some desperate coding and legally questionable sneaking of files between systems, they were able to reconstruct the key on Linux and re-split it properly on Solaris.

The company was saved from catastrophe by noticing an obscure compatibility issue between operating systems. It was a hard lesson about the risks of rolling out untested changes and not having proper backups. PayPal learned to be more careful with their crown jewels and not rely on clever schemes alone for security.

The story illustrates how a single overlooked technical detail can have huge consequences. Something as basic as passphrase handling differed between platforms and almost brought down a multimillion dollar company overnight. Meticulous testing and defense in depth are essential when protecting critical systems. This tale will no doubt be retold within PayPal engineering for decades as a reminder of the need for thoughtful design and redundancy when it comes to security.

*source of information:* [*https://max.levch.in/post/724289457144070144/shamir-secret-sharing*](https://max.levch.in/post/724289457144070144/shamir-secret-sharing)