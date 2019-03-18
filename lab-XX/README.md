# Lab XX - Install minishift and oc binary

## Task 1: Install minishift

The minishift installation is pretty similar to the minikube installation.
Just run this command.

```
brew cask install minishift
```

After the installation you can start your minishift instance. This will take
a while.
> Make sure that virtualbox is installed on your host.

```
minishift start --vm-driver virtualbox
```

After the installation you will get a confirmation that your minishift is started.
The installation will prompt you with a login. The URL in the example beneath is
not necessarily your URL. So do not blindly copy it from this lab.

```
The server is accessible via web console at:
    https://192.168.99.100:8443/console

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin
```

It could be that the `oc` command is not installed yet. You can do this with the
following steps.

Download the `oc` binary at

```
https://github.com/CCI-MOC/moc-public/wiki/Installing-the-oc-CLI-tool-of-OpenShift
```

If you click the `MAC Openshift oc download` it will automatically download the
binary you need to your default download folder.

Browse to the download folder via your terminal and do the following commando in
the folder you recently downloaded. `openshift-origin-client-tools-v1`

Now do the following command.

```
mv oc /usr/local/bin/
```

Now you are able to login to your minishift with the credentials given by the
instance.

In order to get access as an admin to our webconsole we need to add the following addon to minishift.

```
minishift addon apply admin-user
```
