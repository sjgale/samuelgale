---
layout: post
title:  "Viewing locally hosted web pages on your desktop from your phone"
date:   2017-04-26 12:10:13 -0600
categories: jekyll update
---
Previewing a local build, hosted on your desktop, from your phone can be tricky.

In the past, I would just deploy the changes I wanted to test to a server somewhere and navigate to that address from my phone's browser. While that works, it's adds a few additional steps to previewing even the smallest of changes from your mobile device. Sometimes it would be nice if your phone could just see everything your computer saw in it's browser, local builds and all!

Luckily, that's totally possible! And you should be able to set it up in 10 minutes or less.

I chose to use MITProxy to accomplish this because it's an open source tool (it's free, and I'm cheap), easy to run from your cli and works with a number of different OSs. Another benefit of this is it will allow you to monitor all requests being made from your phone to the internet, granting you deeper insight into what's really going on behind the scenes of your favorite apps and sites your visiting.

### Initial Install Instructions:
* Install **mitmproxy** on your computer:
	* See: [http://docs.mitmproxy.org/en/stable/install.html](http://docs.mitmproxy.org/en/stable/install.html)
	* Using homebrew: `brew install mitmproxy`
* Find your computer’s IPv4 address
	* On MAC you can hold option while clicking the network icon in the tray
* Start up mitmproxy from your chosen cli (you can set the port using the -p option): 
	`mitmproxy -p 8888`
	You'll need to leave this running while you want to access sites from your desktop.
* Make sure your phone and Mac are using the same wifi
* Configure your phone to use the proxy to access the network
	* **iPhone:**
		* Go to the Settings -&gt; Wi-Fi
		* Tap the blue arrow next to your current network to access the network settings
		* Find the HTTP Proxy settings and select Manual.
		* Enter your IPv4 Address and the port your chose to run your proxy on
		* Save these changes
	* **Android:**
		* Go to settings -&gt; Wi-Fi
		* Long hold on your current wifi network to open and modify the network settings
		* You may need to choose to view the advanced options
		* Update the Proxy Hostname as your computer’s IPv4 address, update the Proxy Port to the port you chose to run your proxy on
		* Save these changes
* On your phone navigate to [mitm.it](http://mitm.it) and install the appropriate certificate for your device (on iPhones, you may need to use Safari to do this)
* You should now be able to monitor all requests from your phone and access sites available to your desktop (eg. mysite.dev and localhost)

### Instructions for subsequent use:
* Repeat **steps 3 and 4** of the initial Install Instructions

**Also note:** This approach doesn't just work for phones, you can also allow other computers in your network to access this proxy and view your local builds with a few updates to their network settings. This article will point you in the right direction: [https://kb.netgear.com/25191/Configuring-TCP-IP-and-Proxy-Settings-on-Mac-OSX?cid=wmt_netgear_organic](https://kb.netgear.com/25191/Configuring-TCP-IP-and-Proxy-Settings-on-Mac-OSX?cid=wmt_netgear_organic)