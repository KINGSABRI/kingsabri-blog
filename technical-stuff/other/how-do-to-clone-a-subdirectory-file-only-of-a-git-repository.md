# How do to clone a Subdirectory/File only of a Git Repository

I didn't want to clone the whole SecLists repo, but I needed some directories only

```
mkdir wordlists && cd wordlists
git init
git sparse-checkout init
git remote add -f origin https://github.com/danielmiessler/SecLists.git
git sparse-checkout add "Discovery"
git sparse-checkout add "Fuzzing"
git sparse-checkout add "passwords/Default-Credentials"
git sparse-checkout add "Passwords/Common-Credentials/10-million-password-list-top-10000.txt"
git pull origin master
ls
```

```
cat .git/info/sparse-checkout 
Discovery
passwords/Default-Credentials
Passwords/Common-Credentials/10-million-password-list-top-10000.txt
Fuzzing

```



**Source**

* [https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository](https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository)
