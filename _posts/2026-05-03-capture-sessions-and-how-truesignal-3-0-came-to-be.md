---
title: "Capture Sessions, and How TrueSignal 3.0 Came to Be"
description: "What happens when 'I want to prove this to my ISP' turns into the headline feature of a 3.0 release."
date: 2026-05-03
author: "Dave Schwind"
---

*Or: what happens when "I want to prove this to my ISP" turns into the headline feature of a 3.0 release.*

---

One of the best parts of building TrueSignal has been hearing from folks who actually *use* it. Folks doing real things, in real places, with real connections that *actually misbehave in real ways* — not the kind of misbehavior the bars at the top of your phone are good at telling you about.

And, almost universally, the same question kept coming back:

**"How do I prove this to my ISP?"**

That's the question that launched TrueSignal 3.0. And specifically, that's the question that became Capture Sessions...the headline (and coolest!) addition since the app launched.

**TL/DR:** TrueSignal 3.0 is live. The big new thing is Capture Sessions — a Pro feature that lets you record a witnessed timeline of your connection quality and export it as a PDF you can hand to your ISP. There's a cleaner Monitor screen, a reorganized Pro hub, and a pile of polish fixes. If you just want to grab the update, hit the App Store or Google Play and skip the rest of this post (no hard feelings!). If you want the build story, keep going.

---

## The problem with "we don't see anything wrong on our end"

Anyone who's ever called their ISP knows this line. *We don't see anything wrong on our end.*

Sometimes it's true! Sometimes the issue *is* on your end (did you pay your bill??). But often enough, it isn't. Often the problem is somewhere between you and the ISP's monitoring gear...which means *they* don't see it, but you live with it every day. Calls drop. Streams stutter. That all-hands meeting freezes at the worst possible moment.

The ugly truth is that ISPs aren't malicious here. They genuinely don't see it. Their monitoring runs at the head-end and shows their gear is up. They're not lying when they tell you everything looks good on their end...but everything *also* looks bad on yours, and there's no shared language for that conversation.

Capture Sessions is an attempt at building that shared language.

## What Capture Sessions actually does

You pick a server (or just use the default). You pick a duration — anywhere from 1 to 60 minutes. You hit start. TrueSignal pings the server every 2 seconds and renders a candlestick chart of your connection quality, second by second, scrolling right to left like a trading terminal. Green candles when things improved compared to the last bucket. Red when they got worse. The recording is locked once you start it — you can stop early or pause, but you can't extend (more on why in a moment).

When you're done, you save the recording. You give it a name and an optional note ("Zoom call dropping during 1pm meeting"). And then — this is the part that matters — you can export it as a PDF.

The PDF is what I keep calling the **artifact**. It's got TrueSignal letterhead. It's got the chart. It's got a methodology disclosure (ping rate, bucket size, sample count, pauses). It's got an executive summary in plain English. It's got an ISP talking-points section. It's got a full timestamped timeline table at the end.

It's a piece of paper (or a file) you can attach to a support ticket and watch the conversation change.

## The interesting design decisions

A few choices in Capture Sessions probably deserve explaining, because they were *not* the default thing to build.

### Locked duration

Once a recording starts, you can't extend it. You can stop early. You can pause (and the pauses are visible on the chart — more on that in a second). But if you started a 15-minute recording and at minute 14 your connection finally has its bad moment, you can't tack on another 15 minutes to "get a better one."

This was a deliberate philosophical choice. **The artifact has to be defensible.** If users could keep recording until they got the result they wanted, the resulting PDF would mean less. By locking duration up front, every Capture Session represents a fair witness — *this is what happened during the window you committed to, no fishing*.

### Honest gaps

iOS does *not* let backgrounded apps reliably ping things on a schedule. This is a hard platform constraint and there's no clean way around it. We tried. Many times. If you switch apps during a recording, TrueSignal's ping engine hard-stops. We don't fake samples to fill the gap. We don't pretend nothing happened.

Instead, we render the gap *on the chart* as a visible band, document it in the metadata ("Pauses: 1, 23 seconds total"), and call it out in the PDF export. **The honest version of the data IS the data**. If your ISP looks at a Capture Session export and sees a 23-second pause, that's part of the story...not a flaw to hide.

(I'll be honest...some part of me wanted to smooth the values if there was a small interruption. It would *look* prettier. It would *feel* more complete. But it would also be a small lie, and the entire pitch of TrueSignal is that it doesn't lie to you. So...no smoothing for Capture Sessions!)

### Locked methodology

Ping rate is fixed at 2 seconds. Bucket size is fixed at 6 seconds. You can't tune either of these. Users get to pick the duration and the server. Everything else is locked.

This one took me a while to commit to. The customization-loving developer in me wanted to expose every knob. But every knob exposed is a knob someone could turn to game the result, and the artifact stops being defensible the moment someone could ask "but what if you'd set the ping rate higher?" Locked methodology means every Capture Session in the world produced by TrueSignal 3.0 uses the *same* settings. Statistical consistency across captures matters more than per-capture flexibility.

(There's a metaphor here about how the most useful tools constrain you. I'll spare you the philosophy and just say: lock the methodology, ship the feature.)

### Helpful hints

To get the most accurate reading, you need to stay in one location and avoid using the phone for other things. Remember, your connection can vary not just by your external factors, but also by what's happening inside your phone. So, when you're doing a test, it's best to keep the phone steady, don't walk around with it (you'll get different readings in different locations) and resist the urge to use TikTok!

### It's not just about the ISP

Proving something to your ISP was the use case for Capture Sessions, but just like anything, the way it's *actually* used can vary immensely. To be honest, I've gone to various locations in my home and property just to see what the connection is like. For example, I have a large metal outbuilding and I've never figured out exactly what my connection is like out there, between being on the edge of my WiFi and the metal of the outbuilding. Capture Sessions is really fantastic for getting a granular diagnosis of what's going on.

Long story short...if you downloaded the app, purchased Pro, you may be as nerdy as me about this stuff. Or, just super curious. Either way, I'm sure you'll find ways to use this function, and the app overall, that I haven't thought about. If you've figured out something really neat, or maybe you've thought "wow, I wonder if the app could do..." please drop me a note! I love hearing from users!

## The other 3.0 stuff

Capture Sessions is my favorite function of the app thus far, so I'm a bit excited about it. But 3.0 also includes:

A **cleaner Monitor screen.** Same status dot, same metrics, more breathing room. The QoE card is gone (its information lived elsewhere already). The interval selector buttons are gone (Connection Sentinel handles that automatically and better). The result is a Monitor screen that does one thing — *show you whether your connection is good right now* — and gets out of the way. I wanted to get back to the basic "am I connected or not" question. What someone gets for free is exactly that: "am I connected?" They are welcome to, and encouraged, to dig into the Pro functions, but for a basic "am I connected?" this does it in as clean and simple a manner as possible.

A **reorganized Pro hub.** Connection Log is its own first-class destination now, not buried inside other screens. Pro features have icons that aren't borrowed from Ionicons, the cartoon-looking icons that are seemingly everywhere. My icons are custom SVG, designed to feel like TrueSignal rather than feel like everyone else's app.

**Polish fixes throughout.** Some you'll feel even if you don't notice them. Some you'll never notice and that's fine, because the only people who would notice are the people who'd be annoyed if I didn't fix them. (I noticed.)

## What's not in 3.0 (yet)

A few things on the cutting room floor for now, since we're being honest:

**Cloud sync of Capture Sessions.** Recordings live on-device. This is partly a privacy thing (TrueSignal doesn't have a backend, by design — see [the privacy post]({% post_url 2026-04-26-why-truesignal-doesnt-know-where-you-are %})) and partly a "let me get v1 out the door" thing. We can revisit if folks want it.

**Screenshot detection.** Taking a screenshot during a recording can briefly inflate measured latency by 50-100ms because of how iOS prioritizes the JS thread during capture. The fix is a small native module to flag affected samples, and it's on the list. Not in 3.0. (I'll write that one up as its own post — it's a fun rabbit hole.)

**Android parity.** 3.0 is iOS first. Android catches up shortly...the same code is there but the build pipeline takes a little longer. Maybe next week? I can't control Google's review process, or even make predictions on the timeline. But...don't worry, Android friends! I haven't forgotten about you!

## The thing I'm asking for

If you've made it this far...thank you. Genuinely. The fact that anyone reads these posts at all is one of the consistently *coolest* things about doing this.

Try Capture Sessions. Run a recording. Export the PDF. Send it to your ISP, or just send it to yourself for a record. Tell me what works and what doesn't. **TrueSignal Pro is less than a single (small) cup of coffee** and Capture Sessions is the new headline reason to have it.

And then — please — send feedback. What works? What's confusing? What did you wish the PDF had on it? Where would you use a longer recording window? Is 60 minutes too short? Should we add a 4-hour mode for the truly patient?

How does it work for you?

I read everything. The folks in California, in Queensland, in Iceland, and in places I haven't heard from yet — your stories are the reason this app exists, and the reason it'll keep getting better.

There's something *really* cool in the works for 3.1 too...but more on that another day.

Dave
