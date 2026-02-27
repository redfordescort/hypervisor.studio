# Introducing the Game AI Transparency Framework

90% of studios are using AI. 85% of players say they hate it. Developers fear for their jobs. Only Steam tries to require disclosure, and they only cover what players see, not what's behind the scenes. The EU AI Act's transparency requirements hit in August. South Korea's AI Framework Act is already live. The window for the industry to self-regulate is closing fast.

I am a game developer, experienced AI/ML practitioner, and avid player. I'm introducing how I would solve this problem: the [Game AI Transparency (GAIT) framework](https://hypervisor.studio/gait/).

GAIT is a voluntary self-disclosure of how AI is used in game development. It has ratings levels (ESRB-style), but also details of AI use (think Nutrition Facts). The idea isn't to shame the use of AI, but rather to be clear and transparent in how exactly it's used. The system is designed to give us a shared language we lack right now.

## Some Interesting Parallels
When I was thinking about this problem, I realized I had crossed paths with similar problems twice before in my life.

### The Independent Craft Brewer Seal
I am a proud San Diegan, and like so many men of a certain age in this area, I got into homebrewing, about 20 years ago. This hobby connected me to the broader world of craft brewing, which has a surprising amount of connective DNA with game development - brewers are makers, full of creativity but constantly fighting for opportunities in an industry that doesn't always treat them right.

At the height of the craft beer craze (late 2010's), big beer companies were acquiring smaller craft breweries en masse. This presented an "authenticity crisis" for beer buyers; one might stumble into a bar with 15 apparently "craft" beer taps of various brands and styles, and you might think these were legitimate craft or local brands, not knowing that all of those beers are owned and produced by AbInbev, for example.

The independent beer response to this was the Independent Craft Brewer seal, created by the Brewer's Association. The BA created a set of criteria to define an "independent brewer" (based on ownership structure and production volume), and licensed this seal to those brewers, who could use it on their beer packaging and in their breweries. It was a signal to the relevant constituents (brewery owners, staff, and buyers) of the authenticity of the independent, local, and craft nature of what's being sold.

This reminds me a lot of what is going on right now - a crisis of authenticity, not of ownership but of development. Ultimately, the craft beer label didn't impact sales on the macro level. 72% of drinkers said it was important, but sales data showed virtually no difference. But what it did achieve was give a shared vocabulary to an industry dealing with an identity crisis.

### Mortal Kombat and the ESRB
Another inspiration for GAIT is the ESRB, who oversees video game ratings in the US. I'm not saying I caused the ESRB to form, but I'm not not saying that.

When I was 9 years old, I wrote a letter to Nintendo of America, asking them politely to consider allowing Mortal Kombat II to feature blood when it was released for the SNES. Mortal Kombat was becoming famous then for its over-the-top violence and gore; Nintendo had decided to mandate the game take out its most violent content, and change the blood to "sweat" using a palette swap.

In the response from Nintendo, the customer service representative alluded to working being done by Nintendo and its industry peers, in response to inquiries from the US Congress, to establish a rating system for video games. This would become the ESRB. The backdrop to this was a series of hearings in Congress into violence in video games, with Mortal Kombat and the FMV game Night Trap being used as representative examples of the level of explicit violence children who played video games were being exposed to.

The threat presented to game makers was legislative regulation; self-regulating via the ESRB headed off that threat. While there's no governmental mandate that games be labeled with ESRB ratings in the US, they are required de facto in that major game platforms and resellers require ESRB ratings in order for games to be sold.

While it could come to pass that the US Congress could step in and do something again with AI in games, the reality of politics in 2026, relative to 1994, is that Congress is seen by the public as dysfunctional and incompetent. So that feels unlikely to happen. But the regulatory pressure isn't going to come from Congress, it's already coming from the EU and from South Korea, with deadlines months away, not years.

## What is GAIT
Structured AI disclosure in games is effectively non-existent as of now. Steam requires disclosure of AI content, but this is an open text field based on an honor system. No other major marketplace has disclosure requirements. Mobile games have zero disclosure requirements on any storefront.

In the last year alone, four major studios were caught shipping AI-generated content - Ubisoft, 11 Bit Studios, Sandfall Interactive, Frontier Developments. They all used the same excuse of "a placeholder accidentally shipped". When so many studios are doing the same thing accidentally, it's not a problem of carelessness. It's the absence of any structured system for tracking and discussing AI use.

My hope is that by introducing a framework and driving adoption, AI disclosure can become a standard practice, even if storefronts are reluctant to embrace them directly.

See more [here](https://hypervisor.studio/gait/), but in short, the features of the framework include:

1. Clear definitions of AI usage types, with six AI use levels spanning from "absolutely no generative AI used in production" to "Live generative AI is used while you are playing the game"
2. Defined "red lines" that no studio that adopts GAIT is allowed to cross - unconsented creative replication, concealing AI use, mandatory AI safeguards for minors
3. Player-meaningful descriptions of how AI is used

With the exception of the red lines, the framework is meant to be neutral towards AI - the question it tries to answer is "how are studios using AI", and not "should studios use AI". While player and individual developer sentiment is very negative right now towards AI (contrasted with generally positive sentiment from studio leaders), I expect sentiment will change over time as AI tools become increasingly ubiquitous. There is no definition of what the "correct" GAIT level for a studio should be, as accepted norms could be higher or lower later as the AI conversation evolves.

One intention of GAIT is to require participating studios to maintain documentation of AI in their development process and pipelines. My read on the "accidentally shipping AI placeholder" problem is that these are genuinely accidental incidents, but it demonstrates the gap: documentation rigor is still behind as AI rapidly matures. 

There is an explicit carve out for accessibility use cases in GAIT, which is important given the 429 million players with disabilities in the world. One interesting area of innovation is AI-assisted accessibility features, and the exemption is intended to prevent an accidental chill on accessibility feature development.

## Call to action

If you think this is something that should be adopted:

* Players: hit up the makers of your favorite game and see if they'd be interested in sharing their GAIT level.
* Developers: show this to your project and studio leads and ask them to adopt GAIT for your project.
* Studio leads: check out the framework and its overlaps with upcoming regulatory requirements, and see if adopting GAIT now will help you stay compliant.

Go check out the framework [here](https://hypervisor.studio/gait/), read through the full framework, play around with the badge maker. Tell me what's missing - gait-framework@hypervisor.studio.

thanks,
james
*written by my hand. AI was used for reviewing and copyediting, but did not directly edit this text. AI was used to convert my markdown to HTML. So, I guess GAIT 1.5?*

p.s. I publish a daily TLDR-style game industry newsletter at readgg.com