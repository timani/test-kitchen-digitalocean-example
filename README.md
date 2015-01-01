# KitchenCI :Digitalocean example

An example of the Test Kitchen Driver for Digital Ocean with the chef-zero provisioner.

This is based on the test-kitchen-digitalocean driver by that uses [API V2](https://developers.digitalocean.com/) of the Digital Ocean API

# Requirements

The libraries that are required have been included in the Gemfile within the project. However you will need access to additional information such as the Access Key and SSH Key ID from your Digital Ocean Account. 

> [DigitalOcean](https://digitalocean.com/) account.
> Digital Ocean - Access Key 
> Digital Ocean - SSH Key ID
> Chef-zero 
> Test Kitchen Digital Ocean Driver

# Installation and Setup

You'll need to install the gem on your development machine. If you do not have an environment where ruby is installed, the recommended environment is this ruby based docker image. 

```Bash
gem install kitchen-digitalocean
```

or add it to your Gemfile if you are using [Bundler](http://bundler.io/)

```ruby
source 'https://rubygems.org'

gem 'test-kitchen'
gem 'kitchen-digitalocean'
```

At minimum, you'll need to tell test-kitchen to use the digitalocean driver.

```ruby
---
driver:
  name: digitalocean
platforms:
  - name: ubuntu-12-10-x64
```

You also have the option of providing your credentials from environment variables.

```bash
export DIGITALOCEAN_ACCESS_TOKEN="1234"
export DIGITALOCEAN_SSH_KEY_IDS="1234, 5678"
```

Note that your `SSH_KEY_ID` must be the numeric id of your ssh key, not the symbolic name. To get the numeric ID
of your keys, use something like to following command to get them from the digital ocean API:

```bash
curl -X GET https://api.digitalocean.com/v2/account/keys -H "Authorization: Bearer $DIGITALOCEAN_ACCESS_TOKEN"
```

Please refer to the [Getting Started Guide](http://kitchen.ci/) for any further documentation.

# Default Configuration

The driver now uses api v2 which provides slugs for image names, sizes, and regions.

Example configuration:

```ruby
---
platforms:
- name: debian-7-0-x64
  driver_config:
    region: ams1
- name: centos-6-4-x64
  driver_config:
    size: 2gb
# ...
```

# Private Networking

Private networking is enabled by default, but will only work in certain regions. You can disable private networking by changing private_networking to
false. Example below.

```ruby
---
driver:
  - private_networking: false
```

# IPv6

IPv6 is disabled by default, you can enable this if needed. IPv6 is only available in limited regions.


```ruby
---
driver:
  - ipv6: true
```

# Development

* Source hosted at [GitHub](https://github.com/test-kitchen/kitchen-digitalocean)
* Report issues/questions/feature requests on [GitHub Issues](https://github.com/test-kitchen/kitchen-digitalocean/issues)

Pull requests are very welcome! Make sure your patches are well tested.
Ideally create a topic branch for every separate change you make. For
example:

1. Fork the repo
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

# Authors

Created and maintained by [Greg Fitzgerald](https://github.com/gregf/) (<greg@gregf.org>)

***Special Thanks:***

[Will Farrington](https://github.com/wfarr/kitchen-digital_ocean), His fork was a help during the creation of my api v2 driver.

# License

Apache 2.0 (see [LICENSE](https://github.com/test-kitchen/kitchen-digitalocean/blob/master/LICENSE.txt))

