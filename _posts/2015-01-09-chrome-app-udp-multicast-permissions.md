---
layout: 	post
title:      "Chrome App UDP Multicast Permissions"
subtitle:   "Adhoc Documentation"
categories:	javascript
---

Now that the `chrome.socket` API has been deprecated, you should now be using `chrome.sockets.tcp`, `chrome.sockets.tcpServer`, and `chrome.sockets.udp`. With this change comes a change in how you give your app networking permissions in your manifest file. <!-- more -->Previously, if you wanted to allow your app to make a UDP sendTo(), your manifest file would look something like this:

{% highlight json %}
{
    ...
    "permissions": [{
        "socket": [
            "udp-send-to"
        ]
    }]
    ...
}
{% endhighlight %}

To give these same permissions for use with `chrome.sockets.udp` API, you need to change your manifest file to look like the following:

{% highlight json %}
{
    ...
    "sockets": {
        "udp": {
            "send": "*"
        }
    }
    ...
}
{% endhighlight %}

Now say you utilize UDP multicast functionality in your app and you want to make the conversion to the new API. You would previously have had `"udp-multicast-membership"` in your list of permissions under `"sockets"`. You can replicate those permissions for the new API by adding `"multicastMembership": ""` to your `"sockets"` section like this:

{% highlight json %}
{
    ...
    "sockets": {
        "udp": {
            "multicastMembership": ""
        }
    }
    ...
}
{% endhighlight %}

That's all fine and dandy and makes sense but unfortunately it's not currently in the Chrome Developer [Manifest File Format](https://developer.chrome.com/apps/manifest/sockets) documentation. The only place I was able to find this documented was in an [API test](https://code.google.com/p/chromium/codesearch#chromium/src/chrome/test/data/extensions/api_test/sockets_udp/api/manifest.json&type=cs&sq=package:chromium) in the Chromium project. I figured I'd try to save someone a little time. 