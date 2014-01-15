dota2rails-deploy
=================

Contains ansible/vagrant deployment stuff for dota2rails and alacrity repos

vagrant up --no-provision

Notes:

* If you vagrant up, vagrant destroy, vagrant up, you will have the wrong ssh key for the new servers still in your known\_hosts, remove it with `ssh-keygen -f ~/.ssh/known_hosts -R 10.0.0.2` and 10.0.0.3

* Ansible uses a forwarded ssh agent to access github repos (for installing ruby) on the virtual machines, so you must be running this from a machine that has an ssh key registered with github.com and with password already input. If provisioning fails on talking to github, run `ssh -T git@github.com` locally and enter your passphrase to save it to your keyring.

Places you need to enter your info (in the ansible folder):

* group\_vars/all: s3 credentials and steam api key

* group\_vars/matchurls: steam account login info *and steam guard code*

* group\_vars/mqservers: your email sending account

* whatever other values in group\_vars or hosts or Vagrantfile that you wish to change

Things to confirm are running:

* nginx

* unicorn

* app.js (via nodejs forever)

* celery

* rabbitmq

* mongodb

Places to check for errors:

* /var/log/nginx/error.log

* /webapps/dota2rails/log/production.log

* ~/.forever/(4 random characters).log (matchurls/steam login issues)

## Thanks

* <https://github.com/leucos/ansible-rbenv-playbook>

* <https://github.com/owainlewis/vagrant-ansible-rails>
