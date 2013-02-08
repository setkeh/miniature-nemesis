---
layout: post
title: Stop SSH and SFTP timeout
description: Stop SSH and SFTP timeout when SSH into a remote machine
---
Just add the following line to /etc/sshd_config (on the machine you’re SSHing into):

{% highlight sh %}
ClientAliveInterval 60
{% endhighlight %}
	
Next time you SSH of SFTP you’ll be sending ‘keepalive’ packets every 60 seconds.
