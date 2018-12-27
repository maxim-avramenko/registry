Private Docker Registry
=======================

Sometimes you don't want to share your awesome application code with other world.

Private registry for docker images with your application code inside the image lets you restrict access by login and password.

You must use TLS encrypted connection

For example you can use [CloudFlare](https://cloudflare.com) service for your hub.mydomain.com

to play with private registry on localhost add domain name to system hosts file (/etc/hosts for Linux users)

Set up steps:

    * create user and password
    * run init script

Usage:

    $ ./adduser <username> <password>
    $ ./init <domain.name>

Example:

    $ ./adduser maxim MyStrongSecretPassword123 \
        && ./init hub.mydomain.com

After registry service start you can use your credentials to login and push/pull docker images:

    # login to your new private registry
    $ docker login hub.mydomain.com
    Login: maxim
    Password: MyStrongSecretPassword123

    # for example pull ubuntu:18.04 from public registry and push it to your private
    $ docker pull ubuntu:18.04
    $ docker tag ubuntu:18.04 hub.mydomain.com/ubuntu:18.04
    $ docker push hub.mydomain.com/ubuntu:18.04
    $ docker rmi ubuntu:18.04 hub.mydomain.com/ubuntu:18.04

    # check that you have no more ubuntu:18.04 images
    $ docker images

    # pull ubuntu:18.04 from your hub.mydomain.com registry
    $ docker pull hub.mydomain.com/ubuntu:18.04

Now you have your own private registry for docker images.

You can add more users if you want, use:

    ./adduser <username> <password>

