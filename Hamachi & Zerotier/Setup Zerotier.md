Ok, I originally made a guide for this on a Google Doc, and it worked fine, but I prefer to use GitHub rather than Google Docs for things like this.


# Guide to Setting Up Zerotier One (on Windows)
Well first of all, you're obviously going to need Zerotier One.
You can download that [here](https://www.zerotier.com/download/).
There shouldn't be any kind of wizard or anything to press or setup so just install it.


Zerotier will automatically be in the System Tray on the right side of your taskbar, most likely at the bottom of your screen (is taskbar moving still a thing?).
Right click the little Zerotier One icon and you will see something like [this](Reference-Pictures/Zerotier-System-Tray-Overview).
Click the "Join Network" button, and a little window like [this](Reference-Pictures/Zerotier-Join-Network) will pop up.
Don't click any of the extra boxes, and just copy and paste this (9f77fc393e3f074f) into the text box and click the "Join" button.


Windows will then pop up a box on the right side of your screen that looks like [this](Reference-Pictures/Windows-Network-Popup).
Just click the "Yes" button.


Aaaaand we're done... if we were just the end user.
There is still a bunch of stuff we can and probably should do as the Network Owner.
This should be in it's own section but I can do that later...

# Guide to Setting Up Zerotier (on Zerotier Central)
Oh.
We're doing this now I guess.


**YOU CAN ONLY DO THIS IF YOU OWN A NETWORK**


Go to [Zerotier Central](https://my.zerotier.com/network) and login to your account and click on the network you want to edit.

Change the name so that it's easy to distinguish between multiple networks (if you need to).
Change your Access Control to PRIVATE, rather than PUBLIC, as if anybody sees your Network ID, they can join with full access to ping people and connect to other people's computers.
You can change your Managed Route through the IPv4 Auto-Assign.
Personally I like to use (10.244.*.*) as I find it easy to remember and type out.
Don't touch IPv6, and just scroll all the way down to the Flow Rules.


**What are Flow Rules?**


Flow Rules are essentially just codes that tell Zerotier to send traffic to places, or allow or disable some traffic.
Part of our group uses Teamspeak, and I wanted to absolutely be sure that Zerotier is not our problem if Teamspeak breaks.
Teamspeak has a bunch of ports that it uses (443, 6654 30033, 10011, 10022, 10080, 10443, 41144), and I wanted to add them to the flow rules in Zerotier.
To tell Zerotier to accept them, I added this to the flow rules:
```
# Teamspeak Port Routing
accept ztdest 129450b482 and dport 443
      and dport 9987
      and dport 30033
      and dport 10011
      and dport 10022
      and dport 10080
      and dport 10443
      and dport 41144
;
```
There's nothing else to change in Zerotier Central so that will be the end of this guide (finally).
