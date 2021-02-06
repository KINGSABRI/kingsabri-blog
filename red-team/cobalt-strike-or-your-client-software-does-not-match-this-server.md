# Cobalt Strike \| Your client software does not match this server

If you had the chance to work with Cobalt Strike, you'll know that every new version is loaded with cool features plus long waited and weirdly missing feature\(s\) in the older version\(s\).

In most application, especially for those who love Metasploit, once a new release gets released we hurry up to update; but this is not the case with Cobalt Strike, Cobalt Strike requires the client and the server \(teamserver\) to have the same version in order to connect. If you were just like me and jumped to \`cobaltstrike/update\`, you may not be able to connect to your team server again during a running engagement which is SUCK. The Cobalt Strike client will pop up "Your client software does not match this server", just like the following message.

![](../.gitbook/assets/image%20%284%29.png)

Thankfully, I had a snapshot for an older version so I made a new snapshot for the newer version and I kept older image for version compatibility. However, you don't need to do so. Thanks to [ramen0x3f](https://twitter.com/ramen0x3f), she told me that I can keep both versions in different directory, as far as they both have the same license `~/.cobaltstrike.license`.

The best approach I ended up with is to copy the directory before any update and name it with its version

```text
cp -a cobaltstrike cobaltstrike-3.13
```

Then update the default one "cobaltstrike" directory

```text
cd cobaltstrike/
./update
```

then copy the newer version too keep compatibility if any update came up later

```text
cd ..
cp -a cobaltstrike cobaltstrike-3.14 
```

and keep the default directory \(i.e cobaltstrike\) always up to date, but take a copy before any update.

I also updated the `update` script in cobaltstrike to remind me when I update as follows:

```bash
read -n1 -p "Did you take a backup for the current version? [y,n]: " answer
if [[ $answer == "Y" || $answer == "y" ]]; then
        echo -e "\n[+] Updating Cobaltstrike"
        java -XX:ParallelGCThreads=4 -XX:+AggressiveHeap -XX:+UseParallelGC -jar update.jar $*
else
        echo -e "\n[!] Well, go backup it first. cp -a ../cobaltstrike ../cobaltstrike-version";
        echo -e "\n[!] exiting the update process."
        exit 0
fi
```

That's it :\)

