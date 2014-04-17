atlas-playbooks
===============

Ansible playbooks and Vagrantfile for the Atlas of Economic Complexity.

Setting Up a Development Environment
------------------------------------

To easily install a virtualized dev environment from scratch:
- Get Virtualbox: https://www.virtualbox.org/wiki/Downloads
- Get Vagrant: http://www.vagrantup.com/downloads.html
- Install ansible globally with `sudo pip install ansible` (or use easy_install instead of pip).
- Double check that the installs worked by running `ansible` and `vagrant` in the command line.
- Put a bzip-compressed atlas db dump into the vagrant_shared directory and name it atlas_dump.sql.bz2.
- Run `git clone https://github.com/makmanalp/atlas-playbooks && cd atlas-playbooks && mkdir atlas && vagrant up`
- Sit back and wait till all the stuff downloads. It'll download a 350mb VM
  image, around that much more for all the required python and ubuntu packages.
  Should take around 15 minutes.
- Finally, run `vagrant ssh` to get in, then `cd /srv/atlas/` and `source
  env/bin/activate` to get into the virtualenv. Then go in `django_files` and
  run `manage.py runserver 0.0.0.0:8000`. The 0.0.0.0 is important to get
  django to answer requests on ports other than within the virtualbox
- Go to http://127.0.0.1:8000/

Usage Info
---------
- There are two shared directories with the VM. Any change made within the VM
  reflects to the outside of the VM, and vice versa.
    * `vagrant_shared/`: For moving over large SQL dumps etc.
    * `atlas/`: Contains the main source for the site, a checkout of the
      observatory_economic_complexity repo. You can code on this.
- Run "vagrant ssh" to get into the box.
- Run "vagrant help" for more info on how to stop, start, reload, destroy the virtual box.
- If you need to run ansible manually, try: http://docs.ansible.com/guide_vagrant.html#running-ansible-manually
- If you want to make ansible do more stuff, check out the ansible module index: http://docs.ansible.com/modules_by_category.html
- There are also port forwards for the services running inside the VM.
    * 8000: main HTTP server
    * 3307: mysql
