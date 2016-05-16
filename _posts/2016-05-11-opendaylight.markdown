---
layout: post
title:  "OpenDayLight Installation"
description: OpenDayLight is an SDN controller that is funded by the Linux foundation and is feature rich, making it a popular choice for a SDN controller
comments: true
date:   2016-05-11 16:05:18 +0100
---

OpenDayLight is an SDN controller that is funded by the Linux foundation and is feature rich, making it a popular choice for a SDN controller. This tutorial will walk you through installation of OpenDayLight Beryllium Controller on an Ubuntu VM with mininet installed on it. Instructions on setting up the Mininet VM can be found [here](http://www.brianlinkletter.com/set-up-mininet/). I would recommend installing a graphical desktop like LXDE once you have set up the VM. 

### Environment Dependencies for ODL
+ A Java 7- or Java 8-compliant JDK
{% highlight plain %}
mininet@mininet-vm:~$ sudo apt-get install openjdk-7-jdk
{% endhighlight %}
+ Maven 3.1.1 or later for building projects
{% highlight plain %}
mininet@mininet-vm:~$ sudo apt-get install maven
{% endhighlight %}
+ Install git if you don't have it
{% highlight plain %}
mininet@mininet-vm:~$ sudo apt-get install git-core
{% endhighlight %}
+ Add JAVA_HOME to your bash profile or zsh profile by issuing the command 
{% highlight plain%}
mininet@mininet-vm:~$ echo "export JAVA_HOME=/usr/lib/jvm/default-java" > ~/.bashrc
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
{% endhighlight %} 
You have successfully installed opnedaylight if you get the prompt `opendaylight-user@root>`

Next, we have to install features for the OpenDayLight controller. A full set of feature list is available at [here](https://www.opendaylight.org/opendaylight-features-list). Install essential features by issuing the command-
{% highlight plain %}
opendaylight-user@root>feature:install odl-l2switch-switch odl-mdsal-apidocs odl-dlux-all
{% endhighlight %}

To see list of installed features, run
{% highlight plain %}
opendaylight-user@root>feature:list --installed
{% endhighlight %}

That's it! you have ODL set up! 

### Run an SDN Network using Mininet and OpenDayLight

The final step is to test weather OpenDayLight is functioning correctly. By default, if you are using the mininet vm the OpenDayLight Controller is running on IP address `192.168.56.101` and port `6633` respectively. 

On a new terminal, start a mininet topology, specifying the remote controller's IP address and port by issuing the command: 

{% highlight plain %}
mininet@mininet-vm:~$ sudo mn --topo linear,3 --mac --controller=remote,ip=192.168.56.101,port=6633 --switch ovs,protocols=OpenFlow13
{% endhighlight %}

Test weather the connectivity is working by issuing the command on the mininet prompt:

{% highlight plain %}
mininet> pingall
*** Ping: testing ping reachability
h1 -> h2 h3 
h2 -> h1 h3 
h3 -> h1 h2 
*** Results: 0% dropped (6/6 received)
{% endhighlight %}

If you get the same result, your OpenDayLight and Mininet setup is working correctly. 

You can view the GUI of OpenDayLight by opening `192.168.56.101:6633` on your browser. 

![OpenDayLight Login Page]({{ site.url }}/images/posts/opendaylight/ODL-login.png "OpenDayLight Login Page") 
Both the username and password is `admin`. After logging in, you'll see the following screen:
![OpenDayLight DLUX]({{ site.url }}/images/posts/opendaylight/ODL-overview.png "OpenDayLight Console")

Here you can see the miniet topology, view information about the links connecting the different nodes of the mininet topology, the flow entries at the switches etc. This concludes the Installation overview of OpenDayLight. Next up, I'll write about the OpenFlow tutorial using OpenDayLight. Stay tuned ;)
