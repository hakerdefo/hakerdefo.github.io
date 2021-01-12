---
layout: post
title: How to use AhaDNS?
---

## What is AhaDNS?
AhaDNS is a zero logging encrypted DNS server service supporting DNS over HTTPS (DoH) & DNS over TLS (DoT). AhaDNS servers do not log or save any personal DNS request data. AhaDNS servers automatically block Ads, Malware, Trackers, Viruses & Telemetry. AhaDNS is fully open source. AhaDNS is the brainchild of Fredrik Pettersson. Currently AhaDNS servers are located in Netherlands, India and U.S.A.

## How to use it?
Well, answer to this question greatly depend on your application, device and its operating system. In this article I'll cover Windows, GNU/Linux, Firefox and Google Chrome.

### Windows (10, 8, 7)
1. Click the **Network icon** on the bottom right corner of Windows panel toolbar.
2. Click on **Open Network & Internet Settings**.
3. Under **Advanced network settings**, select **Change adapter options**.
4. Right click on the network you wish to change, then click on **Properties**.
5. Choose **Internet Protocol Version 4 (TCP/IPv4)**.
6. Click on the **Properties** button at the bottom right.
7. Select **Use the following DNS server addresses** option.
8. Add **5.2.75.75** (Netherlands) as your **Preferred DNS server**.
9. Add either **45.79.120.233** (India) or **45.67.219.208** (U.S.A) as **Alternate DNS server**.
10. Complete the setup by clicking on the **OK** button.

#### For IPv6 setting first four steps will remain same as above.
5. Choose **Internet Protocol Version 6 (TCP/IPv6)**.
6. Click on the **Properties** button at the bottom right.
7. Select **Use the following DNS server addresses** option.
8. Add **2a04:52c0:101:75::75** (Netherlands) as your **Preferred DNS server**.
9. Add either **2400:8904:e001:43::43** (India) or **2a04:bdc7:100:70::70** (U.S.A) as **Alternate DNS server**.
10. Complete the setup by clicking on the **OK** button.


### GNU/Linux with Network Manager
1. Right click on the **Network Manager icon** in the panel and select **Edit connections**.
2. To change the settings for a wired connection, select the **Wired** tab and/or to change the settings for a WiFi connection, select the **Wireless** tab.
3. Select your **network**, and click **Edit**.
4. Click on **IPv4 Settings** tab.
5. From the drop-down list select **Automatic (DHCP) addresses only** as the **Method**.
6. And in the **DNS servers** field, enter these AhaDNS servers separated by a comma like this,  
`5.2.75.75, 45.79.120.233, 45.67.219.208`
7. Complete the set up by hitting the **Save** button.

#### For IPv6 setup first three steps will remain same as above.
4. Click on **IPv6 Settings** tab.
5. From the drop-down list select **Automatic (DHCP) addresses only** as the **Method**.
6. And in the **DNS servers** field, enter these AhaDNS servers separated by a comma like this,  
`2a04:52c0:101:75::75, 2400:8904:e001:43::43, 2a04:bdc7:100:70::70`
7. Complete the set up by hitting the **Save** button.


### GNU/Linux without Network Manager
1. Open terminal emulator and create a backup of the original configuration file,  
`sudo cp /etc/dhcp/dhclient.conf /etc/dhcp/dhclient.conf.bak`
2. Open **/etc/dhcp/dhclient.conf** file in your favorite text editor as sudo or root.
3. In this file look for a line containing something like this,  
`prepend domain-name-servers 127.0.0.1;`
4. If such a line exists comment it out like this,  
`#prepend domain-name-servers 127.0.0.1;`
5. For IPv4 add following line after it,  
`prepend domain-name-servers 5.2.75.75, 45.79.120.233, 45.67.219.208;`  
For IPv6 add following line after it,  
`2a04:52c0:101:75::75, 2400:8904:e001:43::43, 2a04:bdc7:100:70::70;`
6. Save the file and close the editor. 


### Firefox browser
1. From the Firefox **menu** click on **Preferences**.
2. Go down to the **Network Settings** and click on **Settings**.
3. Go to the bottom and check **Enable DNS over HTTPS**.
4. In the **Use Provider** option select **Custom** and enter any of the following,  
https://doh.nl.ahadns.net/dns-query  
https://doh.in.ahadns.net/dns-query  
https://doh.la.ahadns.net/dns-query
5. Click **OK**.
6. Finally in the address bar enter **about:config** and click on **Accept the Risk and Continue** when prompted.
7. In the search field type **network.trr.mode** and click on **pencil icon** to edit and enter **3** and save it by clicking on **yes check mark**.


### Google Chrome browser
1. From the Google Chrome **menu** open **Settings**.
2. Navigate to the **Privacy and security** section and click on **More** to expand if necessary.
3. **Toggle** on **Use secure DNS** option.
4. Select **With Custom** and in the **Enter custom provider** field, enter any of the following,  
https://doh.nl.ahadns.net/dns-query  
https://doh.in.ahadns.net/dns-query  
https://doh.la.ahadns.net/dns-query


### Android, iOS, MacOS, Microsoft Edge
Guides for these platforms are available at this AhaDNS page,  
[AhaDNS setup guides](https://ahadns.com/setup-guides/ "AhaDNS setup guides")


### Conclusion
You can get more information on AhaDNS from its homepage here,  
[AhaDNS](https://ahadns.com/ "AhaDNS")  

Any question, suggestion, comment on this article are always welcome. You can send them by clicking on the mail icon at the bottom of the page.  
Cheers!!!  

<p xmlns:dct="http://purl.org/dc/terms/" xmlns:cc="http://creativecommons.org/ns#"><a rel="cc:attributionURL" property="dct:title" href="https://hakerdefo.github.io/how-to-use-ahadns/">How to use AhaDNS?</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://github.com/hakerdefo">hakerdefo</a> is licensed under <a href="https://creativecommons.org/licenses/by/4.0?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"></a></p>
