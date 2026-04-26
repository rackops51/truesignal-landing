---
title: "Why Your Bars Lie (And What You Should Look At Instead)"
description: "Your phone shows full bars and you can't load a webpage. Here's what's actually happening, and why those bars in the corner of your screen aren't telling you what you think they're telling you."
date: 2026-05-01
author: "Dave Schwind"
published: false
---

We've all been there. You're standing somewhere...could be a hotel room, could be the parking lot of a Cracker Barrel out in the middle of nowhere, could be the corner of your own kitchen...and your phone shows a healthy three or four bars. Maybe five! You try to send a text to your spouse...nothing. Try to load Google Maps...spinning circle. Check your e-mail...stuck. Even your kids..."why isn't TikTok loading??" After a few minutes of walking in circles, restarting the phone, and muttering some choice words at it, the connection eventually "magically" comes back.

What happened?

Short version: those bars on your phone lied to you. Or, more accurately, they told you the truth about something you weren't actually asking about, but we've been conditioned to believe that what they're showing us means what we think it means (h/t *The Princess Bride* for you movie fans!).

I've dealt with this problem firsthand for years...first in the Navy, then later managing a wind farm out in Rosamond, California (where cell coverage was, at best, "spotty"). I even designed a network connection system (my "4G at Sea" project) for an offshore wind project just so I could ensure phone coverage for windfarm employees, tourists, fishermen, and the Coast Guard.

After walking circles in a shopping mall parking lot trying to get coverage a couple of months ago, I had enough. I've built an app specifically to fix this nonsense.

I'm going to briefly walk you through what's actually going on here, because once you understand it, you'll start spotting it everywhere. (And you'll probably swear at your phone a little less!)

## What the bars are *actually* measuring

The signal indicator on your phone is a representation of something called RSSI...short for Received Signal Strength Indicator. (For LTE and 5G it's technically RSRP, but the basic idea is the same.) Basically, it's a measurement of how loudly your phone hears the cell tower. For Wi-Fi, it's how loudly your phone hears the access point.

That's it. RSSI is just your phone saying "I can hear the radio."

Here's what it does NOT tell you:

- Whether the cell tower has any actual capacity left for you
- Whether the AP's connection out to the internet is healthy
- Whether your ISP is having a bad day
- Whether your phone is working (did you pay your phone bill??)
- Whether the website or app you're trying to reach is even up
- Whether a captive portal is silently holding your traffic hostage
- Whether *any* of your packets are making it through to anywhere

In other words, the bars tell you that your phone and the radio it's talking to can hear each other. Everything past that point (the actual trip out to the internet and back) is completely invisible to that little icon in the corner of your screen.

## Why this falls apart so often in the real world

In the suburbs, on a healthy home Wi-Fi network, with no problems anywhere in the chain...the bars are actually a pretty decent proxy for how things are working. The radio link is usually the weakest part of the connection, so if it's strong, you're probably good.

But out in the real world, the radio link is usually NOT the weakest part. Some examples:

**Hotel and conference Wi-Fi.** Full bars, because the access point is fifteen feet away, mounted on the wall outside your room. Great...except that AP is sharing one overloaded uplink with three hundred other guests trying to stream the big game. Your packets leave your phone fine and then sit in line.

**Cellular at a stadium or concert.** The tower is right there. Your RSRP is excellent. So is everyone else's...and there are 50,000 of them. Towers can only handle so many active users at a time, and you're competing for a slot.

**Captive portals.** Your phone connected to the network and reports a beautiful, healthy connection. The portal hasn't been authenticated yet (you know...that login page that pops up at hotels and airports), so every request is silently getting redirected to a sign-in screen. Your phone has no clue.

**Bufferbloat.** This one's sneaky. The AP is fine, the ISP is up, but somebody on the network is doing a giant upload (cloud backup, OS update, kid streaming Twitch from the basement, whatever) and it's saturating the upstream queue. Latency goes from 20ms to 2,000ms. Web pages load...eventually...and poorly. Video calls fall apart. Bars don't move.

**ISP problems past the modem.** Your router is happy. Your phone says "connected." Your ISP is having a routing issue two hops upstream. There's no mechanism inside your phone for noticing that. The bars are just shrugging.

In all of these cases, your phone is *technically* telling you the truth. It's just answering a question you didn't ask.

## The question you're *actually* asking

When you glance at the connection indicator, you're not really asking "is my radio link healthy?" You're asking something much simpler:

**"Is my internet working right NOW?"**

That's a completely different question, and it requires a different kind of measurement. To actually answer it, something has to *try* sending traffic out and see what comes back. That's called active probing. You ping a target (a server somewhere), measure how long it takes to reply, and watch for failures.

What active probing measures:

- **Latency.** How long does it take for a small packet to make a round trip? Under 50ms is great. Over 200ms feels broken. Over 1,000ms is unusable.
- **Loss.** Are some of those packets just...not coming back? Even small amounts of packet loss destroy real-time stuff like calls and video.
- **Variability.** Is latency steady, or bouncing all over the place? Steady-but-slow is bad. Wildly variable is worse...that's what makes a Zoom call feel like everyone's talking through a robot.

Those numbers actually line up with how a connection *feels*.

## So...are bars useless?

No. (I want to be careful here, because I'm not anti-bars...I'm anti-bars-being-asked-to-do-a-job-they-weren't-built-for.)

RSSI is genuinely useful for one specific thing: figuring out where to stand. If your bars are weak in the basement but strong by the window, that's real, useful information. Same with finding the best corner of a campsite, the right room in a hotel, or which side of the house gets decent cell coverage. For folks who travel a lot or work outdoors, that's not nothing.

But once you've established that the radio is reasonable, the bars have nothing more to tell you. The question stops being "can my phone hear the radio?" and starts being "can the radio hear the rest of the internet?" For THAT question, you need a different tool.

That's the whole reason I built TrueSignal. It pings a target you choose...a public server, your home server, or anything else you trust...every few seconds, measures the response time, and shows you a green/yellow/red status based on what's actually happening to your packets out in the wild. No bars. No guessing. Just response time, on a target that matters to you.

When you measure the right thing, the answers tend to get a lot less mysterious.

---

Anyway...next time you're standing somewhere with full bars and no internet, you'll at least know why. (Knowing won't fix it. But it might save you a lot of muttering at your phone!)

Dave
