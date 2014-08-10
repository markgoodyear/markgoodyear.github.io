---
title: "Better development environments with Vagrant"
excerpt: "Having a properly configured development environment is important to any project; Vagrant does just that."
layout: post
published: true
date: 2014-03-19
---

<p class="lead">Having a properly configured development environment is important to any project; Vagrant does just that.</p>

Before we start, I'm going to assume you are using a Mac for development, but the principles are the same if you're using Windows. It's worth noting Linux users may not have the issues I cover in the post.

## But MAMP rocks!?
I'm a long term user of MAMP, and still use it if I need to quickly fire up a PHP server to test something, though it's not without its limitations. One in particular is that everything may seem perfect on your local machine, but as soon as it's deployed to production, things could break. Why? The main difference here would be the Operating System. As you'll likely be deploying to a Linux server and not OSX/Windows, there may be some compatability issues to iron out. Software (such as Apache, PHP, MySQL etc.) version differences can also cause big problems. From experience, it's best to develop on the same versions of everything to avoid any potential hiccups. The last thing you want is to be fixing unexpected bugs that appear in a different version of PHP—especially after a launch.

Mirroring the production environment as much as possible is an important step to ensure as little as possible can go wrong. As they say; if it can go wrong, it will.

## Other options
Another route I tried is to use the built-in Apache on OSX, along with installing MySQL and multiple PHP versions. Whilst this freed me from MAMP, it was a fairly complicated process and came across a few issues along the way. Replicating the same process on different machines isn't an easy task, not to mention time consuming—especially in a team where everyone would need to have the same setup. If you had two projects with two different software requirements, things start to get complicated, too. So how do we solve these issues?

## Meet Vagrant
Vagrant solves all these issues by allowing us to create portable virtual development environments. This means you can have as many environments as you need, each configured differently to suite the project requirements. So if you need PHP 5.4 on one project and PHP 5.3 on another, Vagrant makes it easy to manage. Replicating an environment on a different machine is as simple as running `$ vagrant up`, saving you the hard work and time of installing and configuring everything manually. Awesome!

Vagrant is easy to configure, so whether you need Apache or Nginx with a specific version of PHP, setting it up is a breeze.

### Getting started with Vagrant
To get started, you'll first need to install [VirtualBox][1]. Once installed, head over to [Vagrant Downloads][2] and grab the latest version.

I won't go into the depths of setting up a project from scratch as there is a great [getting started][3] guide on the Vagrant website. I'd recommend taking a look through the documentation to familiarise yourself with Vagrant and its commands. Rather than learning about dev-ops and creating your own provisioning scripts to provision a Vagrant box, there are many tools out there to get you up and running in minutes. One of my favourites is [Vaprobash](http://fideloper.github.io/Vaprobash/index.html).

Vaprobash uses a collection of Bash scripts to install everything you need to set up your environment. Choosing what you need with Vaprobash is as simple as uncommenting a few lines in the provided `Vagrantfile`, then running a `$ vagrant up`. That's all there is to it, you're ready to code.

Another tool is [PuPHPet][7], an online GUI generator providing a wide range of options. Enter some project info, tick a couple of boxes and `$ vagrant up`. If Vaprobash doesn't offer everything you need, I recommend giving PuPHPet a try.

Both are great options to get started without needing to learn any more than what you would using MAMP. If you need any more flexibility, you can get your hands dirty with provisionging tools—such as [Puppet][5] or [Chef][6]—to completely customise your environment.

### Vagrant workflow
A typical Vagrant workflow would be something like:

1. Initiate a project and `$ vagrant up`. This starts up and configures the virtual machine first time round. Vagrant will take a short while to install everything on this first instance, so grab yourself a coffee while you wait.

2. When everything has installed, fire up your favourite editor and code like a ninja.

3. At the end of the day, either `$ vagrant [suspend|halt|destroy]`. [Suspend][11] will effectively pause the machine, [halt][12] will shutdown the machine, and [destroy][13] will completely remove all traces of the machine like it never existed. Remember to dump the database before destroying so you don't lose it—I've done that far too many times! You can even store it in version control for safe-keeping. Usually you'll only need to destroy a box when a project is complete. Halting or suspending will be fine for the duration. By doing this, `$ vagrant up` will be much quicker as everything is already installed in the box.

## In summary
Vagrant is a great way to create shareable development environments, avoiding the classic line:

> I don't know what you're talking about; it works fine on **my** machine!


[1]: https://www.virtualbox.org/wiki/Downloads
[2]: http://downloads.vagrantup.com/
[3]: http://docs.vagrantup.com/v2/getting-started/index.html
[4]: https://github.com/markgoodyear/vagrant-lamp-base/
[5]: http://puppetlabs.com/
[6]: http://www.opscode.com/chef/
[7]: https://puphpet.com/
[11]: http://docs.vagrantup.com/v2/cli/suspend.html
[12]: http://docs.vagrantup.com/v2/cli/halt.html
[13]: http://docs.vagrantup.com/v2/cli/destroy.html
