# How to create a Github Action to publish a Ruby gem to Rubygems.org



## Step \#1 \| Generate Rubygems API Key

1. Log in to your [rubygems.org](https://rubygems.org/) account
2. Go to **Settings** 
3. Click on **API KEYS**
4. Click **New API key**

{% hint style="danger" %}
Copy your key in a safe place you can't retrieve it from rubygems.org later.
{% endhint %}

![](../.gitbook/assets/image%20%2820%29.png)

## Step \#3 \| Create a Secret for your GitHub repository

1. In your Github _repository_, go to **Settings**
2. Go to **Secrets** from the sidebar 
3. Press **New repository secret** button
4. In the **Name** field put: **GEM\_HOST\_API\_KEY**
5. In the Value field put your rubygems API key
6. Press **Add secret** button

## Step \#4 \| Create a GitHub Action

1. In your repository, Go to **Actions** tab
2. Press **New workflow**
3. Select **set up a workflow yourself**
4. Paste the following in it and save

{% code title="gem-push.yml" %}
```yaml
name: Push Ruby Gem

on: workflow_dispatch

jobs:
  release:
    runs-on: ubuntu-latest
    env:
      GEM_HOST_API_KEY: ${{ secrets.GEM_HOST_API_KEY }}
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0 # need all the commits
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: .ruby-version
          bundler-cache: true
      - uses: actions/setup-node@v2
      - name: Configure Git
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
      - name: Bump and Commit
        run: |
          yarn add standard-version
          yarn run standard-version
          git push --follow-tags
      - name: Push to rubygems.org
        run: |
          gem build *.gemspec
          gem push *.gem
```
{% endcode %}

This will create a file under your repository root directory `.github/workflows/gem-push.yml`

5. Under your repository root directory create `.ruby-version`   file and put the ruby version you desire 

6. Under your repository root directory create  `.versionrc.js`  file and put the following 

{% code title=".versionrc.js" %}
```javascript
version_rb = {
  "filename": "lib/[CHANGE-ME]/version.rb",
  "updater": {
    readVersion: function(contents) {
      match = contents.match(/^\s*VERSION = ["'](.+)["']$/m)
      return match[1]
    },
    writeVersion: function(contents, version) {
      currentVersion = this.readVersion(contents)
      // this isn't the most reliable, but meh
      return contents.replace(currentVersion, version)
    },
  },
}

module.exports = {
  "bumpFiles": [version_rb],
  "packageFiles": [version_rb],
  "preset": "angular",
}
```
{% endcode %}

This script will update your repository version 

## Step \# 5 \| Run your Action's workflow

1. Go to **Actions** tab
2. Select the workflow and press **Run**.



## Resources

{% embed url="https://www.tomdalling.com/blog/software-processes/github-workflow-for-automated-gem-releases/" %}

{% embed url="https://www.youtube.com/watch?v=3bz0IR-GDIw" %}

{% embed url="https://andrewm.codes/blog/automating-ruby-gem-releases-with-github-actions/" %}





