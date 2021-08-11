# install Gitlab in Debian 10
install required libraries

    sudo apt-get install openssh-server postfix -y

to remove postfix use:

    sudo apt-get purge --auto-remove postfix


download and install Debian package from https://packages.gitlab.com/gitlab/gitlab-ce

    wget https://packages.gitlab.com/gitlab/gitlab-ce/packages/debian/buster/gitlab-ce_12.6.8-ce.0_amd64.deb
    sudo dpkg -i gitlab-ce_12.6.8-ce.0_amd64.deb


edit the external_url variable in /etc/gitlab/gitlab.rb

    sudo sed -i "s/external_url 'http:\/\/gitlab.example.com'/external_url 'http:\/\/127.0.0.1'/" /etc/gitlab/gitlab.rb

    sudo gitlab-ctl reconfigure


si sale un error el tipo can not read <file> does not exist

    sudo touch <file>

open server in browser:

    firefox 127.0.0.1:8888'



***

## Reduce the postgres database cache

**recommend value is 1/4 of total RAM, up to 14GB.**

postgresql['shared_buffers'] = "256MB"

Reduce the concurrency level in sidekiq

I set this at 15 instead of 25 as I don't have that many commits going on.

sidekiq['concurrency'] = 15 #25 is the default

Disable prometheus monitoring

prometheus_monitoring['enable'] = false

Restart gitlab and test it out:

Run:

gitlab-ctl reconfigure


exit 0

***
# Uninstall gitlab-ce

    sudo gitlab-ctl uninstall
    sudo gitlab-ctl cleanse
    sudo gitlab-ctl remove-accounts
    sudo dpkg -P gitlab-ce
    sudo rm -rf /opt/gitlab
    sudo rm -rf /var/opt/gitlab
    sudo rm -rf /etc/gitlab
    sudo rm -rf /var/log/gitlab
    sudo rm -rf /root/gitlab-cleanse*
