---
layout: 	post
title:      "Downloading All of the Videos in a RSS Feed Using the Command Line"
subtitle:   "An Exercise in Futility"
categories:	exercise-in-futility
tags:		shell
---

For some reason I decided that the best possible approach to downloading all of the videos from a RSS feed was to use the command line. 
What I came up with is below:

{% highlight bash linenos %}
wget -O - '$FEED'
    | grep -o '"https://[^"]*\.mp4"' 
    | awk '{gsub(/"/, "", $0); print $1 "\t-O\tVideo" FNR ".mp4"}' 
    | xargs -n 3 wget
{% endhighlight %}

It's not very complicated but I'll walk through each line.
 
1. Download the XML and send it to the standard output.
2. Pipe the XML into `grep` and pull out all of the video URLs. Leading and trailing quotes were added to the pattern because the feed I was using had the same URL twice per item. Once as an attribute and once as a value.
3. Pipe the matched URLs from `grep` into `awk`, remove the quotes, and define a name for the file. Here I simply numbered the videos "Video1.mp4", "Video2.mp4", ...
4. Pipe the output from `awk` to `xargs` to use each set of URL, "-O", and name as arguments for a `wget` call.