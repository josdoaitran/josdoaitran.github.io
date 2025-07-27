---
layout: post
title:  "My Awesome Terminal on MacBook"
author: donald
categories: [ tips, sharing ]
image: assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 1.png
---

# My Awesome Terminal on MacBook

Currently, I am using a MacBook Pro as my laptop for my daily work. And to make myself more comfortable in the working moment.

I have the habit of stimulating my brain to focus on my work. One of the ways, I usually use to decorate my workstation, and terminal on my MacBook helps me to do that.

My custom terminal should have:

- Attractive Interface
- Auto-Complete

This page was composed with the target to help me improve my writing skills and share you the way I configure my Terminal.

Table of Contents

Instead of using the default Terminal on MacOSX, I installed iTerm2 and use it in my Daily work.

**Iterm2 Link**:

[https://iterm2.com/documentation-one-page.html](https://iterm2.com/documentation-one-page.html)

Here is the original Iterm2 User Interface

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled.png)

And now, I do a couple of steps to make it more awesome. Original source page: https://github.com/romkatv/powerlevel10k

## Install these fonts:

- [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
- [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
- [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
- [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

## Install and setup `~/.zshrc`

Run this command:
`sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 1.png)

In cases, if you already configured your zshrc profile (For instance, you setup `git/npm/python/java`  environment in your zshrc), you can get the message like:

***“Found ~/.zshrc. Backing up to /Users/{your_profile}/zshrc.pre-oh-my-zsh Using the Oh My Zsh template file and adding it to ~/.shrc.”***

It’s meant that your old zshrc profile was backed up to the new folder: ***zshrc.pre-oh-my-zsh***

In order to keep the existing configuration, you can copy the value on ***zshrc.pre-oh-my-zsh to new ~/.zshrc***

## Install **zsh-autosuggestions** and **Zsh-syntax-highlighting** plugin on ZSH

- Run 2 below commands:

```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```
git clone [https://github.com/zsh-users/zsh-syntax-highlighting.git](https://github.com/zsh-users/zsh-syntax-highlighting.git) ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- Add **zsh-autosuggestions** and **Zsh-syntax-highlighting**  into **config plugins** of **zshrc** profile

Open `~/.zshrc` file by this command: `vi ~/.zshrc`

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 2.png)

## Install `powerlevel10k`

Run this command:

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

## Restart your iterm2 application

You can restart your iterm2 by: quite your iterm2 and open it again.

You can follow the setup wizard of powerlevel10k

- Select Yes to install more Font

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 3.png)

Follow the hint, we Quick your iTerm and open it again.

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 4.png)

- After you open iterm2 again, you can see Setup Winzard and follow to choose proper options as below:

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 5.png)

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 6.png)

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 7.png)

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 8.png)

Then, you can see the result in your iterm2 like below:

![walking]({{ site.baseurl }}/assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 9.png)

## Configure again your terminal

You can configure again your terminal setting by running this command:

```latex
p10k configure
```

And then you can follow the wizard to set up again the setting configuration on your terminal

                                   — Copyright 2024 — 

