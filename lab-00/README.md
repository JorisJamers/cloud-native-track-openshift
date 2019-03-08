# Lab 00 - Prerequisites

In this lab we will be installing the OpenShift CLI tools, better know as the 
`oc` command.

## Task 1: Downloading the binary

Download the binary from the following location:

https://mirror.openshift.com/pub/openshift-v3/clients/3.11.93/macosx/oc.tar.gz

```
curl -o ~/oc.tar.gz https://mirror.openshift.com/pub/openshift-v3/clients/3.11.93/macosx/oc.tar.gz
```

## Task 2: Unpack the binary

Unpack the binary into a directory in your `PATH` variable, in the command 
below we unpack the binary to `/usr/local/bin`:

```
tar -xvzf oc.tar.gz -C /usr/local/bin/
```

## Task 3: Make binary executable

In order to properly use the binary we need to make it executable:

```
chmod +x /usr/local/bin/oc
```

## Task 4: Basic CLI configuration

The easiest way to initially setup the OpenShift CLI is to use the
`oc login` command. It’ll interactively ask you a server URL, username
and password. The information is automatically saved in a CLI configuration file 
that is then used for subsequent commands.

```
oc login
```