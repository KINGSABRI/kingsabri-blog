# Changing VMware Workstation tmp file in Linux

## Introduction

Regularly, I'm getting an error message from VMware workstation when my `tmp` directory consume the whole partition space. This freezes the running machines and closes all machines.

So I decided to change VMware default directory to another disk.

### Step \#1 \| Close VMware workstation

First, close VMware workstation and make sure that there is no background process running.

### Step \#2 \| Edit Vmware Configurations

Open to vmware configuration file as `root` user using your favorite editor.

```text
nano /etc/vmware/config
```

Then add the following line.

```text
tmpDirectory = "/your/new/vmtmp/"
```

Note: It's recommended to make a new directory and not make the temp files hanging with your other files.

### Step \#3 \| Run VMware Workstation

Now run VMware workstation and fire-up a machine. You'll immediately see a new directory being created for that machine

## **Source**

* [https://communities.vmware.com/thread/164084](https://communities.vmware.com/thread/164084)

