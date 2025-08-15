+++
draft = false
date = 2025-08-15T12:50:24-04:00
title = "from ...files to dotfiles"
description = ""
slug = ""
authors = []
tags = ["dotfiles"]
categories = []
externalLink = ""
series = []
+++

# Intro
Around three years ago, I removed Windows and replaced it with Ubuntu as my main OS. Additionally, I started moving away from GUIs in favor of the terminal. A key reason for this shift was Neovim. What enthralled me about both—and what I think other people found attractive—was the customizability: you could make them as minimal or extravagant as you wanted. The cherry on top was the idea of dotfiles, the hidden configuration files that customize a Linux or macOS system.

However, I eventually became so obsessive about productivity that I became less productive. In this post, I'll share how I made the mind shift from viewing dotfiles as an always-unfinished configuration (hence the "..." in ...files) to a tool that truly aids my productivity on any machine.

# Baby Steps
A primary area where I got stuck was my Neovim config. I would read online about all the ways I could change the editor: add the filetype to the status line, update the colorscheme, and so on. But when you're up until 4 a.m. "optimizing" your config, it's probably not that serious. I found that the issue wasn't the changes themselves, but that I was focusing on all the things I could change instead of the things that would allow me to focus.

My solution was to start small. I commented out all the custom configuration and started with vanilla Neovim. As I used the editor, I'd notice what was impeding my focus. One of the first things was the glaring default colorscheme, which was hard on my eyes. So I changed it, and continued using a minimal Neovim plus the new colorscheme. I repeated this process, adding one customization at a time as the need arose. I found that I was spending more time using the editor than modifying it.

# If It Ain't Broke
> "The greatest enemy of a good plan is the dream of a perfect plan."
> **— Carl von Clausewitz**

My Neovim experiment taught me a powerful lesson: you don't need to fix what isn't broken. After a few weeks of this new process, I had a stable, usable configuration. I stopped adding new features and focused on what was working. I wasn't spending my time on Reddit or GitHub looking for the next best plugin; I was actually using my tools to get work done. I didn't need a perfect plan—a "good enough" one was better because I could start using it immediately. The goal of dotfiles shifted from constant optimization to functional stability.


# Staying Busy
This mindset eventually extended beyond my Neovim config. When I started exploring new command-line tools, I applied the same principles. For example, instead of spending a weekend researching and configuring a complex tool like Zsh with a dozen plugins, I just installed it and started using it with its default settings. When I noticed a recurring task that was cumbersome—like navigating directories—I'd look for a simple plugin to address that specific pain point. This approach prevented me from getting lost in a sea of options. I was no longer busy "customizing"; I was busy being productive. The time I saved not tweaking my setup was time I could spend coding, writing, or learning something new.

# Conclusion
The journey from Windows to Ubuntu and from GUIs to the terminal was an exciting one, but the real breakthrough wasn't in the tools themselves—it was in my relationship with them. I had to let go of the idea that my dotfiles were a perpetual project that needed constant tinkering. By adopting a "just enough" philosophy, my configuration stopped being a source of distraction and became a stable foundation for my work. My dotfiles are no longer an obsessive pursuit of an impossible ideal; they are a living document of the customizations I've genuinely needed.
