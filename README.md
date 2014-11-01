# Automate WordPress installation with HHVM + Nginx + Varnish in Ubuntu 14.04

Also optimized to work fine with WordPress permalinks.

## About Varnish

Varnish Cache is an HTTP accelerator (also known as a caching HTTP reverse proxy) and a useful tool for speeding up a server, especially during a times when there is high traffic to a site.

It works by redirecting visitors to static pages whenever possible and only drawing on the server itself if there is a need for an active process.

In this automation Varnish is really optimized to don't cache the ``wp-admin``/``wp-login`` and invalidate the cache of pages and posts every time them are modified.

This occurs when editing, publishing, commenting or deleting an item, and when changing themes.

## Extra features

- FTP Server to auto-install plugins, themes, etc
- SMTP Server to be allowed to send mails
- Best permalink format configured for SEO

## Requirements

**Ansible:** http://docs.ansible.com/intro_installation.html#installing-the-control-machine

## Installation with Vagrant

Vagrant creates a new virtual machine

Install the following dependencies:

- VirtualBox: https://www.virtualbox.org/wiki/Downloads
- Vagrant: http://www.vagrantup.com/downloads.html
- Vagrant plugins: (*Install them executing in a shell the following commands*):
    - ``vagrant plugin install vagrant-vbguest``
    - ``vagrant plugin install vagrant-hostsupdater``

Then execute ``vagrant up`` in your terminal (You must be in this project directory path)

You can access to your new blog opening ``http://blog.vagrant`` or ``http://www.blog.vagrant`` in your browser.

Also you will be able to log-in with ssh in your new virtual machine executing ``vagrant ssh``.

## Local installation in your server

You should run this in your server.

First configure the ``ansible/config/production.yml`` file to set your correct server domains.

Then execute ``ansible-playbook ansible/playbook.yml -c local -i "127.0.0.1, --extra-vars=@ansible/config/production.json"`` in your terminal (You must be in this project directory path)

You can access to your new blog opening ``http://yourowndomain.com`` in your browser.


## Remote installation in DigitalOcean with Packer

Download Packer from http://www.packer.io/downloads.html

And install it: http://www.packer.io/intro/getting-started/setup.html

(It's simple, move the downloaded packer binary in to /usr/local/bin/, or into the binary path which you want)


Create a new copy of the packer.json.dist file: cp packer.json.dist packer.json

Create a new Personal Access Token from https://cloud.digitalocean.com/settings/tokens/new

And change the following line in your new packer.json.dist:

```
"api_token": "put_your_digitalocean_api2_token_here",
```

Then execute: ``packer build packer.json.dist``

This will create a new digitalocean image (https://cloud.digitalocean.com/images) ready to use (You can use this image when you create a new droplet)
