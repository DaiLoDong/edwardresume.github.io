---
title: Self-hosted Web Apps and Custom Domain
date: 2019-09-16
links:
  - type: site
    url: https://donger.ca
tags:
  - Docker
  - Linux
  - Networking
  - Cloudflare
---

What started as a way to play games with friends during COVID (RIP Hamachi) turned into a dozen self-hosted apps my friends, family, and I actually use every day.
<!--more-->

## How it started

I've always had an itch to tinker, and COVID gave me the time to scratch it. The first version of this project was a handful of self-hosted game servers. Just somewhere free and open 24/7 so my friends and I could play during whatever ungodly hour we wanted.

Being a hoarder of old computer parts, it was easy to piece together a Windows Server as a guinea pig. It hosted a private TeamSpeak 3 server for voice comms, headless Steam servers, and some private file sharing.

That's where I learned why "it works on my LAN" doesn't mean it works on the internet, and about a dozen other lessons that only stick when your friends are annoyed on Discord because Minecraft is down and it's your fault.

## Graduating to Linux

Buying my first home meant more space and more opportunity to take the project seriously. It also felt like the right moment to stop hiding behind a familiar OS, so I committed to learning Linux properly. I picked Debian on the recommendation of a friend who works as a computer repair technician. He assured me Debian was well documented and it's been the foundation of my infrastructure since I took his word for it (thanks David).

## Where it is today

The current platform runs 30+ containerized web apps across three machines, all orchestrated with Docker and managed centrally through **Komodo**. The mix has grown well beyond game servers. There's a private media server, photo backup, document tools, PDF utilities, collaborative whiteboards, and a self-hosted Google ecosystem replacement, just to name a few. A handful of them are now part of my family's daily routines.

### Reliability

Buying new plants at the garden centre is easy. Keeping them alive is hard.

**Beszel** handles the systems, **Uptime Kuma** covers the services, and **Apprise** hoots and hollers on Discord and email when something is wrong. Dashboards are no good if I have to stare at them all day. I did all this to do less work, not more.

The setup has stayed above 99.90% uptime over the last 12 months. Three 9s of reliability out of a closet server is something I'm pretty proud of.

Getting there meant learning how things actually fail (auto-updates were a surprisingly big offender), how to troubleshoot quickly, and why backups are not a waste of disk space. The real payoff, though: no more texts from my in-laws saying "the photos are broken."

### Security

You know how your parents used to tell you there are bad people on the internet? Well... they're right, and unfortunately castle doctrine doesn't apply online.

Anything that needs to be reachable from the internet sits behind **Cloudflare Tunnels** acting as a reverse proxy, so my home network is never exposed directly. Most public-facing apps are gated by **Cloudflare Access** policies with **GitHub OAuth** as the identity provider, which gives me real authentication on apps that were never designed to have it.

## Just buy a subscription

First and foremost, I do it for myself. I use these apps multiple times a day and they genuinely make my life easier. I also hate ads with a passion and refuse to pay for subscriptions. Bring back buy it once!

The more interesting answer is that this has been one of the best ways I've found to learn and experiment. A lot of what I run into here (orchestration, monitoring, security, debugging weird failure logs at 1 AM) shows up in some form in my professional work as a data engineer. Getting reps in at home has made me noticeably better at it during the day. You also develop a spidey sense for when something's off. That instinct has saved a deployment or two.