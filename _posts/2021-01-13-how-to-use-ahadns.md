---
layout: post
title: How to use AhaDNS
categories: [how-to, DNS]
slug: ahadns-tutorial
excerpt: Wanna say Aha to a safer internet? Wanna get rid of those ads, malwares, trackers, viruses & telemetry? Alright then, AhaDNS is here for you.   
---

## What is AhaDNS?

AhaDNS is a zero logging encrypted DNS server service supporting DNS over HTTPS (DoH) & DNS over TLS (DoT). AhaDNS servers do not log or save any personal DNS request data. AhaDNS servers automatically block Ads, Malware, Trackers, Viruses & Telemetry. AhaDNS is fully open source. AhaDNS is the brainchild of Fredrik Pettersson. Here is the list of current locations and addresses of AhaDNS servers,  

|           Location          | IPv4 Address   | IPv6 Address          | DoH Address                                                                                  |
|:---------------------------:|:--------------:|:---------------------:|:--------------------------------------------------------------------------------------------:|
| Netherlands                 | 5.2.75.75      | 2a04:52c0:101:75::75  | [https://doh.nl.ahadns.net/dns-query](https://doh.nl.ahadns.net/dns-query){:target="_blank"} |
| India                       | 45.79.120.233  | 2400:8904:e001:43::43 | [https://doh.in.ahadns.net/dns-query](https://doh.in.ahadns.net/dns-query){:target="_blank"} |
| United States - Los Angeles | 45.67.219.208  | 2a04:bdc7:100:70::70  | [https://doh.la.ahadns.net/dns-query](https://doh.la.ahadns.net/dns-query){:target="_blank"} |
| United States - New York    | 185.213.26.187 | 2a0d:5600:33:3::3     | [https://doh.ny.ahadns.net/dns-query](https://doh.ny.ahadns.net/dns-query){:target="_blank"} |  


## How to use it?

There are multiple ways in which you can say Aha to a faster, spam-free & secure Internet experience via AhaDNS. Let's take a look at a few of them. In this article I'll use addresses of Dutch & Indian servers of AhaDNS but you can use any of the AhaDNS servers listed in the table above.  

### Windows (10, 8, 7):

- Click the **Network icon** on the bottom right corner of Windows panel toolbar.
- Click on **Open Network & Internet Settings**.
- Under **Advanced network settings**, select **Change adapter options**.
- Right click on the network you wish to change, then click on **Properties**.
- Choose **Internet Protocol Version 4 (TCP/IPv4)**.
- Click on the **Properties** button at the bottom right.
- Select **Use the following DNS server addresses** option.
- Add <inline-code>5.2.75.75</inline-code> as your **Preferred DNS server**.
- Add <inline-code>45.79.120.233</inline-code> as your **Alternate DNS server**.
- Complete the setup by clicking on the **OK** button.  

#### For IPv6 setting first four steps will remain same as above.

- Choose **Internet Protocol Version 6 (TCP/IPv6)**.
- Click on the **Properties** button at the bottom right.
- Select **Use the following DNS server addresses** option.
- Add <inline-code>2a04:52c0:101:75::75</inline-code> as your **Preferred DNS server**.
- Add <inline-code>2400:8904:e001:43::43</inline-code> as your **Alternate DNS server**.
- Complete the setup by clicking on the **OK** button.  

### GNU/Linux with Network Manager:

- Right click on the **Network Manager icon** in the panel and select **Edit connections**.
- To change the settings for a wired connection, select the **Wired** tab and/or to change the settings for a WiFi connection, select the **Wireless** tab.
- Select your **network**, and click **Edit**.
- Click on **IPv4 Settings** tab.
- From the drop-down list select **Automatic (DHCP) addresses only** as the **Method**.
- And in the **DNS servers** field, enter these AhaDNS servers separated by a comma like this,
```text
5.2.75.75, 45.79.120.233
```
- Complete the set up by hitting the **Save** button.  

#### For IPv6 setup first three steps will remain same as above.

- Click on **IPv6 Settings** tab.
- From the drop-down list select **Automatic (DHCP) addresses only** as the **Method**.
- And in the **DNS servers** field, enter these AhaDNS servers separated by a comma like this,
```text
2a04:52c0:101:75::75, 2400:8904:e001:43::43
```
- Complete the set up by hitting the **Save** button.  

### GNU/Linux without Network Manager:

- Open terminal emulator and create a backup of the original configuration file,
```shell
sudo cp /etc/dhcp/dhclient.conf /etc/dhcp/dhclient.conf.bak
```
- Open **/etc/dhcp/dhclient.conf** file in your favorite text editor as sudo or root.
- In this file look for a line containing something like this,
```text
prepend domain-name-servers 127.0.0.1;
```
- If such a line exists comment it out like this,
```text
#prepend domain-name-servers 127.0.0.1;
```
- For IPv4 add following line after it,
```text
prepend domain-name-servers 5.2.75.75, 45.79.120.233;
```
- For IPv6 add following line after it,
```text
prepend domain-name-servers 2a04:52c0:101:75::75, 2400:8904:e001:43::43;
```
- Save the file and close the editor.  

### Firefox browser:

- From the Firefox **menu** click on **Preferences**.
- Go down to the **Network Settings** and click on **Settings**.
- Go to the bottom and check **Enable DNS over HTTPS**.
- In the **Use Provider** option select **Custom** and enter the following DNS over HTTPS (DoH) address,  
[https://doh.nl.ahadns.net/dns-query](https://doh.nl.ahadns.net/dns-query){:target="_blank"}
- Click **OK**.
- Finally in the address bar enter **about:config** and click on **Accept the Risk and Continue** when prompted.
- In the search field type **network.trr.mode** and click on **pencil icon** to edit and enter **3** and save it by clicking on **yes check mark**.  

### Google Chrome browser:

- From the Google Chrome **menu** open **Settings**.
- Navigate to the **Privacy and security** section and click on **More** to expand if necessary.
- **Toggle** on **Use secure DNS** option.
- Select **With Custom** and in the **Enter custom provider** field, enter the following DNS over HTTPS (DoH) address,  
[https://doh.nl.ahadns.net/dns-query](https://doh.nl.ahadns.net/dns-query){:target="_blank"}.  

### Routers:

There are way too many routers out there and their setups greatly vary from one another. Sadly, I can't possibly cover them all. You can Search DuckDuckGo or Google for changing DNS settings of your particular router. For this article I'll explain how you can use AhaDNS servers on TP-Link AC1750 router.
- Open your favorite browser.
- In the address bar type <inline-code>tplinkwifi.net</inline-code> and hit Enter.
- Enter your username & password on the login screen.
- Click on the **Advanced** tab. Next click on **Network** menu button on the left side of the screen. And from the **Network** options select **DHCP Server**.
- **Enable DHCP Server** if it is disabled.
- For IPv4 in the **Primary DNS** field enter <inline-code>5.2.75.75</inline-code>
- For IPv4 in the **Secondary DNS** field enter <inline-code>45.79.120.233</inline-code>
- For IPv6 in the **Primary DNS** field enter <inline-code>2a04:52c0:101:75::75</inline-code>
- For IPv6 in the **Secondary DNS** field enter <inline-code>2400:8904:e001:43::43</inline-code>  
- Click on the **Save** button to complete the setup.

### Android, iOS, MacOS, Microsoft Edge:

[AhaDNS iOS setup guide](https://github.com/AhaDNS/setup-guides/blob/master/Apple/iOS.md){:target="_blank"}  
[AhaDNS Android setup guide](https://github.com/AhaDNS/setup-guides/blob/master/Android/Android.md){:target="_blank"}  
[AhaDNS MacOS setup guide](https://github.com/AhaDNS/setup-guides/blob/master/Apple/MacOS.md){:target="_blank"}  
[AhaDNS Microsoft Edge setup guide](https://github.com/AhaDNS/setup-guides/blob/master/MSEdge/Edge.md){:target="_blank"}  


## Verifying your AhaDNS setup:

To verify that you are using AhaDNS servers, open your browser and visit,  
[DNS leak test](https://www.dnsleaktest.com/){:target="_blank"}  
And when the site opens click on **Extended test** button.
When the test completes, you should see the **address** of AhaDNS server you selected in your setup under the **Hostname**.  


## Further help on AhaDNS:

If you need any help regarding AhaDNS setup or have a question or a query about it, you can use any of the following official support channels,  
[AhaDNS Community on Telegram](https://t.me/ahadns_community){:target="_blank"}  
[Official subreddit of AhaDNS](https://www.reddit.com/r/ahadns/){:target="_blank"}  
