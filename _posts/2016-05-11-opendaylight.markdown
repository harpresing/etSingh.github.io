---
layout: post
title:  "OpenDayLight Beryllium Installation"
description: OpenDayLight is an SDN controller that is funded by the Linux foundation and is feature rich, making it a popular choice for a SDN controller
comments: true
date:   2016-05-11 16:05:18 +0100
---

OpenDayLight is an SDN controller that is funded by the Linux foundation and is feature rich, making it a popular choice for a SDN controller. This tutorial will walk you through installation of OpenDayLight Beryllium Controller on an Ubuntu VM with mininet installed on it. Instructions on setting up the Mininet VM can be found [here](http://www.brianlinkletter.com/set-up-mininet/). I would recommend installing a graphical desktop like LXDE once you have set up the VM. 

### Environment Dependencies for ODL
+ A Java 7- or Java 8-compliant JDK
{% highlight plain %}
$ sudo apt-get install openjdk-7-jdk
{% endhighlight %}
+ Maven 3.1.1 or later for building projects
{% highlight plain %}
$ sudo apt-get install maven
{% endhighlight %}
+ Install git if you don't have it
{% highlight plain %}
$ sudo apt-get install git-core
{% endhighlight %}

### Install OpenDayLight
Download the OpenDayLight controller from <a href="https://www.opendaylight.org/downloads">here</a>. 
After downloading, unzip the file to your desired destination folder:
{% highlight plain %}
$ unzip ~/Downloads/distribution-Beryllium-SR1.zip -d ~/Your-Destination-Path
{% endhighlight %}
cd into the unzipped folder and run
{% highlight plain%}
$ ./bin/karaf
{% endhighlight %} You have successfully installed opnedaylight if you get the prompt `opendaylight-user@root>`

Next, we have to install features for the OpenDayLight controller. A full set of feature list is available at [here](https://www.opendaylight.org/opendaylight-features-list). Install essential features by issuing the command-
{% highlight plain %}
opendaylight-user@root>feature:install odl-l2switch-switch odl-mdsal-apidocs odl-dlux-all
{% endhighlight %}

To see list of installed features, run
{% highlight plain %}
opendaylight-user@root>feature:list --installed
{% endhighlight %}

That's it! you have ODL set up now.

