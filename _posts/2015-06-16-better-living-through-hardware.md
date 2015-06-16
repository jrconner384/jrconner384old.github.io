---
layout:      post
title:       "Better Living Through Hardware"
date:        2015-06-16 14:51
description: How I bit the bullet and improved my home network.
tags:        home networking, hardware, open source, dd-wrt
---
##Connecting My Home##
I recently bought a new router: the excellent [Netgear R7000 Nighthawk](http://amzn.to/1JWgGzA). My motives were pure. I couldn't get a decent wireless signal a mere 15 feet from my old router, let alone across the house at my bedroom TV. My wireless bandwidth was typically less than 2.0Mbps (yes, that's intentionally a lower case 'b').

I tried everything I could think of short of buying something. I examined the wireless signals in my neighborhood to see which channels were relatively unoccupied so I could stake a claim there.

I trolled the internet looking for any idea of how I could configure my router using [dd-wrt](www.dd-wrt.com) firmware, which provides much better control than any stock firmware most (less expensive) routers have.

I even set my phone right next to or on top of the router hoping that would do something magical.

No dice. My Ethernet connections worked blazingly fast but that meant only four machines in my living room would reliably work so our phones and tablets would never be able to take any real advantage of the network.

##Shopping For Dummies (i.e. me)##
I'm not computer illiterate by any stretch of the imagination, between spending most of my working life in IT support and, more recently, getting a CS degree and spending a few years as a software engineer.

Despite that, some hardware has always been a black box to me. I know enough to at least smell hints of marketing lies disguised as ground breaking features and, in a competetive enough market, I generally assume that there's some justification for some subset of the products to be more expensive (though there are some [notable exceptions](http://bit.ly/1gqpkut) to this idea).

#The Old Me: Slapdash Consumer#
It had been a while since I purchased a router and I've never given it too much thought. I usually paced up and down the router aisle at Best Buy or Target, read boxes, and stood around looking pensive, hoping that would lead to me making a smart decision. My priorities were always not having too few Ethernet ports, not spending too much money, and getting the latest 802.11 standard.

That's an okay set of criteria for thrifty people and those who don't get too invested in the state of their home network. For me, a budding home systems administrator, it was time to up the ante.

#The New Me: Responsible Consumer#
__Old Habits__

I still wanted to avoid spending "too much" money, but that's different for everyone and changes at intervals. The kid in me that loves gadgets wanted to spend 50% more money on the [R8000 Nighthawk](http://amzn.to/1G1bHce) or some similar high-end consumer model but I tempered that instict. The model I went with, though cheaper than the R8000, was still two-to-three times more expensive than any router I'd bought in the past. I decided it would be worth it _if_ I didn't get a lemon, though this was the one bullet point I spent the most time sitting and thinking about.

Despite at least half of my devices sitting on the 802.11n standard, I obviously didn't even look at anything less than the current 802.11ac. It's backwards compatible all the way back to 802.11a and all of my ac devices will have the best possible tech at hand. I'm also prepping for the day I can finally get fiber service and take better advantage of the bandwidth this hardware can deliver.

As for the Ethernet port count, four is and always has been the standard, though I would have liked and could easily make use of eight. There was no real sticking point here, though, since this is an even lower priority than the price.

__New Thinking__

_Firmware Support_

I'd already been using dd-wrt on my old router but I was also aware of Tomato, so one goal behind my search was getting an idea of which is better liked, more widely used, more regularly updated, more thoroughly supported, and more feature rich.

Since I can't determine how many people use each of the popular open source solutions, I'll just tell you that my cursory research gives dd-wrt that point.

Some sources (which I neglected to bookmark, sorry) said that Tomato hasn't been updated in years. I also found two different packages going by that name and, honestly, wasn't interested enough in changing to a different firmware to figure out what was going on there.

That's now two points for dd-wrt.

I was going to check which firmware supported the router I wanted but I'd already ruled out Tomato so I just confirmed that dd-wrt works with the R7000.

Three points and the win to dd-wrt.

_Stock Firmware_

It probably seems weird to talk about stock firmware after deciding to use something after-market, but I had solid reasons to care about this.

I wanted to get an idea of the sort of power user features I could get out of the box. The R7000 appeared to offer more than the expected set of features in the stock firmware and I couldn't quickly find a demo online so I decided it would be good enough if it came to it. Mainly, I needed to know I'd be happy with the stock firmware if I didn't have success with dd-wrt.

_Crowdsourcing Opinions_

Customer reviews are a big factor for me, especially for more complicated consumer goods like computer hardware. I started with this [CNET](http://cnet.co/1GcrQL1) article to get one guy's opinion as a launchpad into my own research. The router I chose didn't even make that list but an hour on Amazon reading reviews and looking at similar products (as well as the highest rated products, I almost always start by sorting search results by best ratings) led me to my choice.

The [most enlightening review](http://amzn.to/1KWOL3o) was actually from a network engineer (an expert on this sort of hardware) and she only rated it at 2/5 stars. The salient points, though, are that she has an unusually complex home network and she probably got a lemon. She admits that she got a lemon, though, and says you'll be very happy if you don't get a lemon, too.

The review was a mixed bag but this one sold me on the decision as much as all of the five star reviews. I always get a little suspicious when a product gets nothing but five star reviews so it was good to see that somebody had taken a really critical eye to the product. It was much easier to digest the positive statements in that review knowing she said that stuff despite being ultimately disappointed.

_Bonuses_

The R7000 has two USB ports, a 3.0 in the front and a 2.0 in the back. This wasn't a requirement for me and I've already got my home network set up with a couple of easily accessible places to drop files but the idea of centralized NAS was appealing.

It also has three antennas. I have enough skepticism to wonder if this is actually useful or even harmful, but my last router had no antennas so some superstitious part of me latched on to that idea.

If I stuck to the stock firmware, Netgear has an app called [Genie](http://bit.ly/1nmKzep) which offers some sort of remote control over the router. I had a super easy time flashing it with dd-wrt, though, so I never even got around to trying the app. Even though this wouldn't hit my list of requirements, it earned a brownie point by my estimation.

Both dd-wrt and the stock firmware can be attached to a [DDNS](http://bit.ly/1elq0Sk) provider like [no-ip](www.noip.com). I haven't explored the full depth of possibilities here but I'd already done some magic with no-ip to get in to my home network from outside so this was an appealing perk.

_The Scorecard_

- Has 802.11ac
- Has four Ethernet ports
- Is on the list of dd-wrt compatible devices
- There are plenty of side perks

##Unboxing Day##
Setup couldn't have been much easier. I plugged it in and splashed around in the stock firmware to get a feel for it and I was reasonably pleased but, ultimately, I decided I'd stick with the original plan to use dd-wrt.

I'm not going to go too much in depth about flashing your device with dd-wrt here. They say on the site that it's a complicated process and there's pretty much always a chance you'll brick your device. They also advise users to always follow the directions on the appropriate pages on their site rather than anything a third party posts.

I will point you at [this readme](http://bit.ly/1Flbgbd), which is where I started. That readme is linked from a [post dated 10-13-14](http://bit.ly/1N0misA) on the dd-wrt message boards.

Here's the high level view, though. I backed up the stock firmware, followed the instruction labeled "Netgear Firmware", then the one labeled "DD-WRT already installed". Those instructions are unusually terse, which worried me since flashing my old router took an hour or more and pages upon pages of reading, but that was really all I needed. It was only a few steps, less than fifteen minutes, and no 30/30/30 resets, which were the biggest pain in the neck in flashing my old hardware.

##Conclusion##
This is day four with the router and I'm still happy with it. Since I was using dd-wrt before, it was super easy to set the new router up to behave like the old one. There are two particularly big benefits, though: my TVs at the far end of my house can now reliably connect wirelessly without the repeater I'd been using and I'm getting over 50Mbps over wireless on a regular basis, which is on par with what I get over Ethernet.
