# How to Set hostname in MacOS

## Step \#1: Open The Terminal

Open the terminal and execute the following

### **Set ComputerName**

ComputerName is the user-friendly name for the system

```text
scutil --set ComputerName  NewHostName
```

### **Set LocalHostName**

LocalHostName is the local \(Bonjour\) hostname

```text
scutil --set LocalHostName
```

### **Set HostName**

Hostname is the name associated with hostname and gethostname

```text
scutil --set HostName
```

## Step \#2: Reboot

Reboot your system to apply and see your changes.

