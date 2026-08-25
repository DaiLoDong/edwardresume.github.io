---
title: Personal Wedding Website
date: 2025-11-12
links:
  - type: site
    url: https://github.com/DaiLoDong/wedding
tags:
  - wedding
  - custom-website
  - front-end
  - back-end
---

When my wife and I started planning our wedding, the frequently advertised "custom" website templates didn't appeal much to me. Paper invites get misplaced, physical RSVP cards can take weeks to arrive (if we're lucky and Canada Post isn't on strike), and the evergrowing FAQ isn't a sustainable solution.

I wanted something better, so I built something better.
<!--more-->

## Why a custom site

I could have used one of the off-the-shelf wedding website builders. They're ok. But "ok" wasn't really good enough for a wedding, much less my own wedding. I wanted one link guests could open, find what they needed fast, and be done. To be honest, I just did not want countless emails with questions.

I am very particular about the user experience. I am one of those users who has a custom config for everything I use. Every feature on the site started as a real question a guest asked us (before the site was even live!), or a real moment of friction I had experienced at another wedding. If it took more than 15 seconds to answer, I considered that too cumbersome.


## What the site does

The site became the landing page for everything wedding related. Some highlights:

### Guest experience

- **Fully responsive design** that works on every device, screen size, and aspect ratio.
- **One-tap RSVP** that writes directly to a Google Sheet via a Google Apps Script REST endpoint. No third-party form service, no signup required.
- **Digital seating chart** searchable by either guest name or table number using a lightweight JS string search.
- **Add to Calendar** with support for Google, iCal, Outlook, and Yahoo.
- **Countdown timer** to build some hype.
- **Embedded venue video** with a fallback image on mobile to keep things fast.

### Travel and logistics

- **Interactive Google Maps** powered by the Google Maps API, showing both the ceremony and reception locations with directions.
- **Google Flights booking button** that auto-detects the visitor's location and pre-fills the origin city and event date.
- **Weather forecast** for the wedding date via a third-party API. The ceremony was outdoors and it's Victoria, so... rain is a real looming threat.

### Event gallery (the crowd favourite)

I wanted our photos kept private, but still open to guests sharing their POV with us. The usual ad infested event camera apps want a subscription, an account signup, and a cloth swatch from the Dalai Lama's robes. Annoying, right? I built my own so guests could upload straight from the site and watch the gallery update live as others did the same.

- A **Cloudflare Worker** handles uploads, retrievals, and CORS headers.
- Image data is stored on a private image host.
- **Cloudflare KV** acts as a lightweight database for metadata.

The result was a shared, real-time photo wall that captured candid moments from dozens of angles I would have never gotten from a single photographer.

### Behind the scenes

- **Automated email alerts** to my inbox the moment anyone RSVPs, handled by Google Apps Script triggering Gmail sends so I always know the expected head count.
- **Custom domain** hosted on GitHub Pages and routed through my own Cloudflare domain, with full DNS control and analytics.

## Retrospective

I learned more building this than I have at some actual jobs. I was designing it, building it, breaking it, and using it (most of the time, all in the same day). It's not often you sit on every side of a project at once, and it makes you a lot more aware of tradeoffs. Sometimes the clean code answer and the good UX answer are different, and you just have to pick. I don't need Pentagon level security, or to do everything with 84 bytes of RAM in O(1) time. That said, getting the Apps Script CORS headers right took embarrassingly long.

The reward was watching it actually work both in the lead up and on the big day itself. Guests were RSVPing within hours of launch, and seeing the gallery fill up live during the reception brought me a lot of joy. A few guests told us, unprompted, that it was the smoothest wedding logistics they'd ever experienced.

With how much weddings cost, it was refreshing to be able to pull this off for free.


## Stack

**Frontend:** HTML, CSS, JavaScript
**Hosting:** GitHub Pages, Cloudflare domain
**APIs & Integrations:** Google Maps Platform, Google Apps Script (RSVP + Gmail automation), Cloudflare Workers, Cloudflare KV, third-party weather API
**Other:** Multi-calendar export