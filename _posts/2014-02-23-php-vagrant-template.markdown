---
layout: post
title:  "PHP Vagrant Template"
date:   2014-02-23 12:10:00
categories: php puppet vagrant devops
---

So I finally got sick of creating new puppet for every PHP project I started.

I created a [template project](https://github.com/PurpleBooth/vagrant-puppet-centos-6.5-php5.5-template) to create a Centos 6.5 VM with PHP 5.5 installed. Should help get new projects off the ground a little faster.  Check it out [here](https://github.com/PurpleBooth/vagrant-puppet-centos-6.5-php5.5-template).

Configuring
-----------

I'd recommend changing the hostname to something descriptive for the projects.

This VM will work out of the box. However to use a hostname applicable you, change [the hostname line](https://github.com/PurpleBooth/vagrant-puppet-centos-6.5-php5.5-template/blob/master/Vagrantfile#L9) in the Vagrantfile
```ruby
config.vm.hostname = "change-me"
```

And rename the heira data file "[puppet/hieradata/change-me.yaml](https://github.com/PurpleBooth/vagrant-puppet-centos-6.5-php5.5-template/blob/master/puppet/hieradata/change-me.yaml)" to match the hostname.

How to use
----------

You probably don't have a base Centos 6.5 image, use [veewee](https://github.com/jedi4ever/veewee) to make one.
```bash
veewee vbox define 'centos-6.5' 'CentOS-6.5-x86_64-netboot'
veewee vbox build 'centos-6.5'
veewee vbox export 'centos-6.5'
vagrant box add 'centos-6.5' 'centos-6.5.box'
```

Then just use it like normal.

```bash
vagrant up
```


Webserver
---------

The doc root is at **/vagrant/web**. You can find the webserver running at [http://192.168.40.13](http://192.168.40.13).

The webroot is the "[web/](https://github.com/PurpleBooth/vagrant-puppet-centos-6.5-php5.5-template/tree/master/web)" directory.


But it doesn't support X
------------------------

This project is supposed to be base you can build your own puppet on. So it can't and won't support everything.

The firewall, for example, is disabled, which isn't suitable for production, so you should probably add production configuration of the firewall when you do that work. Likewise the PHP OPCache isn't running, so you'll want to enable that for you production sites too.
