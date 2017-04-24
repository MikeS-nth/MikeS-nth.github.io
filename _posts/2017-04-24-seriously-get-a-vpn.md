---
layout: post
title: "Seriously, Get a VPN"
feature-img: '../img/sample_feature_img_3.png'
---
There's been plenty of [media attention](https://arstechnica.com/tech-policy/2017/03/senate-votes-to-let-isps-sell-your-web-browsing-history-to-advertisers) lately about the news that the US government has reversed course on internet privacy and now allows internet service providers to *use and sell your browsing history* for commercial purposes.  This has sparked broader interest in using virtual private networks (VPNs) as a way for internet users to protect their privacy.

Let me skip to the point:  you should use a VPN.  It's just a good idea with almost no downside. Even if you're law abiding and have nothing to hide, it doesn't mean you should abdicate any and all privacy and security.  Do you have door locks and window shades?  Then you should use a VPN.

A quick aside:  Please understand that I am **NOT** saying that a VPN = security, full stop.  Protecting your electronic security and privacy is multi-faceted, and there is no silver bullet.  If you're interested in a good primer, I highly recommend the Electronic Frontier Foundation's [Surveillance Self Defense](https://ssd.eff.org) site as a good introduction and basic how-to.

Back to VPNs...why are they useful?  Specifically, a VPN encrypts your internet traffic between your computer (or phone or tablet) and the VPN exit point.  This has two major benefits:
1. Makes it very difficult for a "bad guy" to steal, snoop, or otherwise mess with you on public wifi.  (Be extremely cautious on any public wifi, anyway.)
2. Prevents the internet service provider (or whomever controls that public wifi router) from seeing what websites you visit.

There are many paid VPN services out there that make it pretty easy to set up a VPN by downloading their app and paying a modest subscription.  The most often-cited downside is that these companies can see all your browsing data (even if your ISP can't), and it is possible that they may turn around and sell it.  Also, some popular websites block traffic from known VPN providers, which forces you to disconnect from the VPN and lose all its benefits.  (Would you drop your shields in the Neutral Zone?  I wouldn't.)

If you have the technical knowledge (or willingness to learn it), I suggest setting up your own VPN on a server you control.  This used to be somewhat difficult, but it's become relatively easy, thanks to a cyber security company called [Trail of Bits](https://www.trailofbits.com), who released a free VPN setup tool called [Algo](https://blog.trailofbits.com/2016/12/12/meet-algo-the-vpn-that-works/).  (Not to be confused with algo as in algorithms.  Theirs is named in honor of Al Gore, who invented the internet.)

For my fellow data scientists, enthusiasts, and technical professionals, I would gently suggest that you *should* go the DIY route, because you can do it with your existing command line and cloud computing skills.  (And by that I mean, the very basics of command line and setting up a cloud instance.)

Last night, I got Algo up and running on an Amazon Web Services EC2 Tier 2 Micro instance (free tier, for about a year).  After a little poking around, it took about 30 minutes of work.  So far, I have 5 devices configured to use it, and the others will be done once I have a few minutes to spare.

Algo also works with DigitalOcean (reportedly the most user-friendly), Google Compute Engine, and Microsoft Azure cloud computing services.  With DigitalOcean, for example, $5/month will get you a sufficient cloud instance to be your VPN server.

#### Resources
There are a lot of resources out there for setting up an Algo VPN:

Setting up Algo:

- Algo Github site with downloads and installation instructions: https://github.com/trailofbits/algo
- Lifehacker.com how-to guide (this replicates a lot of the Algo instructions, but I found it easier to use): http://lifehacker.com/how-to-set-up-your-own-completely-free-vpn-in-the-cloud-1794302432

Cloud providers:
- Amazon Web Services: https://aws.amazon.com
- DigitalOcean: https://www.digitalocean.com
- Google Compute Engine: https://cloud.google.com/compute/
- Microsoft Azure: https://azure.microsoft.com/en-us/

Security and Privacy in General:
- EFF Surveillance Self Defense: https://ssd.eff.org
