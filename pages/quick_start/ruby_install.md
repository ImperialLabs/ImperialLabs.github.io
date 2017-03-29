---
title: Step By Step - Ruby Install
keywords: 'getting_started, quick start'
last_updated: 'March 29, 2017'
tags:
  - step-by-step
  - ruby
sidebar: framework_sidebar
permalink: ruby_install.html
folder: quick_start
---

# Ruby Install
When installing locally or using the rake tasks to use the bot, you will need to install ruby v2.3 or later

## Install options
RVM and rbenv are both version managers for ruby, it purely preference for which one is used.

-   [RVM](#rvm) - Install a Ruby version manager
-   [rbenv](#rbenv) - Install a Ruby version manager
-   [System](#system) - Install the native Ruby package

### RVM

-   Website: <https://rvm.io/>

#### Install

```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable --ruby
rvm install 2.3.3
rvm use 2.3.3
```

### rbenv

-   Website: <https://github.com/rbenv/rbenv>

#### Install

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo "gem: --no-document" > ~/.gemrc #(optional)

cat >> '~/.bashrc' << 'EOF'
if [ -d "~/.rbenv" ]; then
     export PATH="$HOME/.rbenv/bin:$PATH"
fi

EOF

cat >> '~/.bashrc' << 'EOF'
rbenv ()
{
    local command;
    command="$1";
    if [ "$#" -gt 0 ]; then
        shift;
    fi;
    case "$command" in
        rehash | shell)
            eval "$(rbenv "sh-$command" "$@")"
        ;;
        *)
            command rbenv "$command" "$@"
        ;;
    esac
}

EOF

cat >> '~/.bashrc' << 'EOF'
eval "$(rbenv init -)"

EOF
```
#### Configure

```
rbenv install 2.3.3
rbenv global 2.3.3
```

### System

For system specific instructions see [Here](https://www.ruby-lang.org/en/documentation/installation/)

### Bundler

Website: <http://bundler.io/>

#### Install

`gem install bundler`

{% include links.html %}
