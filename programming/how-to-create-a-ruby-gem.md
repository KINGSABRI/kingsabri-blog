# How to create a ruby gem

Each time I create a gem I do the same search again and again. I keep saving the URLs in here and there and it’s really getting awkward. So I decided to write my own post about it.

## LT;DR

{% tabs %}
{% tab title="Command" %}
```text
bundle gem GEMNAME
```
{% endtab %}

{% tab title="Result" %}
```
bundle gem GEMNAME
Creating gem 'GEMNAME'...
MIT License enabled in config
      create  GEMNAME/Gemfile
      create  GEMNAME/lib/gemname.rb
      create  GEMNAME/lib/gemname/version.rb
      create  GEMNAME/gemname.gemspec
      create  GEMNAME/Rakefile
      create  GEMNAME/README.md
      create  GEMNAME/bin/console
      create  GEMNAME/bin/setup
      create  GEMNAME/.gitignore
      create  GEMNAME/LICENSE.txt
Initializing git repo in /full/path/gemname
```
{% endtab %}
{% endtabs %}

### Packaging The Gem Into Gem File

```text
cd GEMNAME
gem build GEMNAME.gemspec
```

### Pushing The Gem to Rubygems.org

```text
gem push GEMNAME-0.0.1.gem
```

## **Resources**

* [http://guides.rubygems.org/name-your-gem/](http://guides.rubygems.org/name-your-gem/)
* [https://blog.codeship.com/building-a-well-polished-ruby-gem/](https://blog.codeship.com/building-a-well-polished-ruby-gem/)
* [http://weblog.rubyonrails.org/2009/9/1/gem-packaging-best-practices/](http://weblog.rubyonrails.org/2009/9/1/gem-packaging-best-practices/)
* [http://bundler.io/rubygems.html](http://bundler.io/rubygems.html)
* [http://guides.rubygems.org/command-reference/\#gem-build](http://guides.rubygems.org/command-reference/#gem-build)
* [https://www.engineyard.com/blog/its-raining-gems](https://www.engineyard.com/blog/its-raining-gems)

