---
title: "Why TrueSignal Doesn't Know Where You Are"
description: "An email from a user this morning prompted some reflection on the privacy decisions baked into TrueSignal...and what's coming next."
date: 2026-04-26
author: "Dave Schwind"
---

One of the coolest things about developing this app is hearing from people all over the world who use it. I went to bed last night after hearing about it being used to diagnose home network issues in Iceland and I got an email this morning from a guy in Queensland, Australia, with some very valid questions.

This fellow is a real estate photographer. Lifetime Pro user. He spends his days driving from property to property, shooting interiors and exteriors and drone aerials, and then trying to dump 200+ RAW files to the cloud before his next appointment. He needs a solid connection.

His feedback was simple. Could TrueSignal show him a colored map of where signal strength was good around him? That way, when an upload was failing in one driveway, he could glance at the app and drive to the nearest known-good spot.

This is great feedback and something I'd LOVE to incorporate. But...alas...it's also one TrueSignal *cannot* do. By design.

## The early decision that shaped everything

Early in TrueSignal's design, I had to make a call: should the app know where you are?

There are two camps of users out there...and the camps don't overlap much.

**Camp One** wants location services ON. They want maps, heatmaps, "remember the Wi-Fi at this coffee shop," "tell me if I'm near a known-good signal location." That's a real, valid set of needs.

**Camp Two** wants their phone to mind its own business. No tracking. No location pings sent to anyone. No "we'll only use your location to improve your experience" boilerplate that they've learned to roll their eyes at. They want a tool that does its job and doesn't phone home. (Did you read the recent news story from March 2026 about a French Navy sailor revealing the position of an aircraft carrier — the Charles de Gaulle, no less — by uploading his workout to a fitness app? TrueSignal prevents this, by design.)

Both camps are right, but want and need different things from a connection-quality app.

But you can't really build for both at once. The minute the app knows where you are, the privacy story is gone...even if YOU never abuse the data, even if I never look at it, even if it's never sent off the device. The promise of "this app does not know where you are" is binary. It's either true or it isn't.

I picked Camp Two.

## What "privacy-first" actually means here

A lot of apps say "privacy-first" and then quietly ask for your location, your contacts, push notification analytics, an account with your e-mail, and a Facebook login button "for convenience." TrueSignal's version is shorter:

- **No GPS.** The app does not request location permissions. Not on iOS, not on Android. Ever.
- **No account.** There's no signup, no login, no "create your TrueSignal profile." Open the app and it just runs.
- **You pick the target.** When TrueSignal pings something to measure your connection, you pick what it pings...whether that's a public server, your own home/work server (highly recommended for those who want or need full control), or a target your IT team specifies.
- **No third-party tracking.** Purchase verification goes through RevenueCat (which is unavoidable for in-app purchases), and that's the only outside service the app talks to (and even they don't get actionable data, save for purchase info).

The result is that TrueSignal doesn't know your name. Doesn't know where you are. Doesn't know which networks you've connected to. It *can't*. That's the design.

## The cost is real

For the folks in Camp One (Team "Location is Okay")...I get it.

There's a long list of really cool features I can't add because of how TrueSignal is built. A heatmap of where you've had good signal? Needs location data. A map of "blackspots" near you? Needs location data. (Side note for the Australians and Brits in the audience: "blackspot" is the local term for what Americans call "dead zones." Australia's federal government even has an entire Mobile Black Spot Program funding new towers in underserved areas. Genuinely better word, in my opinion!) "Remember this Wi-Fi network and let me know when we're back in range"? Needs location data.

The folks who want those features are not wrong. They have a real workflow problem – as important as dependable network connection is to TrueSignal.

## What's coming

I hate not having an answer to a nagging question (I've written a few books just because I wanted an answer to a couple of questions!). A few weeks ago, I started designing a sister app. One whose design center is the *other* camp (I see you, Team Camp One!)

Still privacy-respecting in the sense that your data stays on your device. But location-aware in the sense that it can do all the things TrueSignal won't. A personal coverage map. A way to find good signal nearby. Tools for the user who needs to upload from variable places and doesn't want to keep guessing.

It's NOT "TrueSignal with location turned on." It's a different product, with a different design center, for a different user.

I'm not announcing the new app today. (Still in design, and I don't want to over-promise on a release date I haven't earned yet.) But I wanted to put it on the record: if you're in Camp One...the camp that wants the location-aware version...I hear you. I'm working on it. And I'd love to hear from you when it's ready.

## In the meantime

TrueSignal is going to keep doing what TrueSignal does. Tell you whether your connection is actually working RIGHT NOW...and not phone home about anything else while it's at it. The privacy aspect of TrueSignal isn't an accident – it's by design.

If you're a TrueSignal user reading this: thank you. Your support means the world to me. If you haven't downloaded TrueSignal, please do. Check it out. Try the Pro version – it literally costs less than a single (small) cup of coffee. Send me feedback. How does it work for you? Where are you using it? Are there ways it can improve? I love to hear user stories and I love to get feedback.

If you're someone who needs the *other* thing: stay tuned. There's something really cool in progress!

Dave
