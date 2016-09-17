How to run a local instance of the Barcelona 2016 Perl Conference
=================================================================

Quick steps to get a clone a conference ACT and run it locally

Clone Alexm Act vagrant
-----------------------

    vagrant init alexm/Act
    perl -i -pe 's|# config.vm.network "forwarded_port", guest: 80, host: 8080|config.vm.network "forwarded_port", guest: 8080, host: 8080|' Vagrantfile
    vagrant up --provider virtualbox

Clone and prepare the conference repository
-------------------------------------------

    $ vagrant ssh

    vagrant@lucid32:~$ git clone https://github.com/Act-Conferences/barcelona2016.git
    vagrant@lucid32:~$ perl -i -pe 's|^(conferences = .*)|$1 barcelona2016|' ~/Act/conf/act.ini
    vagrant@lucid32:~$ cd ~/act/actdocs
    vagrant@lucid32:~/act/actdocs$ ln -s ~/barcelona2016/actdocs barcelona2016
    vagrant@lucid32:~$ cd ~/act/wwwdocs
    vagrant@lucid32:~/act/wwwdocs$ ln -s ~/barcelona2016/wwwdocs barcelona2016

Start the web server
--------------------

Start the apache web server inside vagrant

    $ vagrant ssh
    vagrant@lucid32:~$ httpd -f ~/Act/httpd.conf

If you change the Act config and/or pages, probably you'll need
to restart apache:

    $ vagrant ssh

    vagrant@lucid32:~ pkill httpd
    vagrant@lucid32:~ httpd -f ~/Act/httpd.conf


Then you should open http://localhost:8080/ye2015/ and see the
Act instance on your computer.


Register User
-------------

The last step is to register user vagrant for the conference and
make then grant them admin rights:

    $ vagrant ssh

    vagrant@lucid32:~$ ~/Act/bin/gengrant vagrant
    vagrant@lucid32:~$ ~/Act/bin/grant_rights admin to vagrant on barcelona2016

Now you can login as user vagrant and password vagrant. Find the
rights administration page under the Users menu.


That's all.

This page is based on https://github.com/alexm/Act-vagrant/blob/master/README.ye2015

