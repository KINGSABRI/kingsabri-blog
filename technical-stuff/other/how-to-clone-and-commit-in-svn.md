---
description: the SVN ops that I need
---

# How to Clone & Commit in SVN

I don't frequently work with SVN, but when I have to, I need the following commands to do my basic operations.

### Clone SVN repo

```text
svn co --username=YOURUSERNAME SVN_REPO_URL
```

### Commit changes

#### Step 1 \| Add all changes 

```text
svn add --force * --auto-props --parents --depth infinity -q
```

or 

```text
svn add * --force
```

#### Step 2 \| Commit all changes

```text
svn commit -m "MyCommit"
```



