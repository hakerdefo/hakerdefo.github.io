---
layout: post
title: Fix slackpkg verification of the gpg signature failed error in Slackware
categories: [slackpkg, slackware]
slug: fix-verification-gpg-error-slackpkg-slackware
---

So you installed Slackware and after selecting a package mirror in <code>/etc/slackpkg/mirrors</code> file, you as root did,  

```bash
slackpkg update
```

But instead of updating the package list, **slackpkg** complained and threw this error,  
<!--more-->

```bash
ERROR: Verification of the  gpg signature on CHECKSUMS.md5
	failed! This could mean that the file is out of date
	or has been tampered with. If you use mirrors.slackware.com
	as your mirror, this could also mean that the mirror to
	which you got redirected is not yet updated with the most
	recent changes in the Slackware tree.
```

First thing you need to do is make sure that the system clock is set to correct date and time. If it is not set to correct time, open terminal emulator and run as root,  

```bash
ntpdate pool.ntp.org
```

This should automagically correct the system time but if for some reason the **pool.ntp.org** server is busy, try the following server,  

```bash
ntpdate time.nist.gov
```

Next just make sure that NTP service is enabled at boot to avoid incorrect date/time in future. In terminal as root do,    
 
```bash
chmod 755 /etc/rc.d/rc.ntpd
/etc/rc.d/rc.ntpd start
```

And finally, as root run the following command to update GPG keys,  

```bash
slackpkg update gpg
```

And the moment of truth,  

```bash
slackpkg update
```

In 99.99% cases the update process would go without a hitch and if it does, don't forget to upgrade your Slackware install,  

```bash
slackpkg upgrade
```

May the **Slack** be with you!  

![May the Slack be with you](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/dare_to_slack.webp "May the Slack be with you")
