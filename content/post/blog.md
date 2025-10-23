+++
draft: false
title: "Starting My Homelab and Automating a Hugo Blog"
date: 2025-10-18
description: "How I set up a Fedora server, automated deployments, and launched a Hugo-based blog to document my DevOps journey."
tags: ["homelab", "hugo", "blog", "automation", "devops", "self-hosting"]
+++

# Starting My Homelab and Automating a Hugo Blog

## TL;DR
Set up a Fedora-based home server, configured GitHub Actions for CI/CD with Hugo, and launched a live technical blog to document my DevOps and automation projects.  

**Live Site:** [rmitchell745.github.io](https://rmitchell745.github.io)  
**Stack:** Fedora Server, Hugo, GitHub Actions, YAML, Git, Markdown  

<!--more-->

---

## Introduction
I’ve always been the techie person in the room when one wasn’t available. As I began planning a career change, I needed a way to **showcase my technical skills** in a real, hands-on way.  

That led me to build a **home lab** and **technical blog** — both as a way to learn DevOps practices and as a platform to document my projects. The first challenge: get this blog built and continuously deployed.  

Next up: developing and self-hosting my first application — a weather notification service.

---

## Setup and Configuration
I started by digging out an old ThinkPad laptop, pulling the family photos off it, and researching Linux distributions.  

I wanted a **Red Hat-based distribution** to align with enterprise environments, so I initially chose **CentOS Stream** for its stability between update cycles. Unfortunately, the hardware was too outdated for CentOS — a good reminder that enterprise distros assume newer infrastructure.  

I pivoted to **Fedora Server**, which offers excellent hardware compatibility for personal and older systems.  

Once installed, I added:
- **Git**
- **Hugo**
- **Neovim**

…and got to work setting up my blog directly on the machine.

> _Image of ThinkPad here_

---

## Blog Automation with Hugo
After comparing options, I chose **Hugo** because it’s fast, fully open-source, and highly customizable via Markdown and simple configuration files.  

Hugo also has strong **GitHub Actions integration**, making it ideal for a command-line and CI/CD-focused workflow.  

Here’s the flow I set up:
1. Initialized a Hugo directory on the server.  
2. Created a Git repository and pushed to GitHub.  
3. Configured **GitHub Actions** for automated builds and deployment to **GitHub Pages**.  

I hit some early 404 and 403 issues, which I traced to repository settings — GitHub Pages must be configured to build from the correct branch. Once fixed, my site went live successfully.

> _Screenshot of GitHub Pages and Actions tab here_

---

## Reflection
After completing this first project, I can confidently say it’s an **excellent introduction to DevOps**.  

Running on real hardware instead of a virtual machine gives you exposure to hardware compatibility, networking, and boot troubleshooting.  

Working with **Hugo** and **GitHub Actions** provides early, meaningful experience with:
- YAML syntax in automation contexts  
- Version control workflows  
- Continuous deployment pipelines  

And the repetition of committing, pushing, and triggering builds reinforces a solid Git workflow muscle memory.

---

## Skills Practiced
- Linux server setup and configuration  
- YAML syntax and GitHub Actions automation  
- Git and version control workflow  
- CI/CD pipeline management  
- Troubleshooting build environments  
- Markdown documentation  

---

## Results
- Hugo site successfully deployed and hosted  
- Dynamic content structure for posts, projects, and home page  
- Working automated workflow from local to GitHub Pages  

---

## Future Steps
- Point domain (`rmitchell.tech`) to the live blog  
- Add project pages with dynamic post listings  
- Automate syncs from dev VM to the live server  

---

## Resources
- [Hugo Documentation](https://gohugo.io/documentation/)  
- [GitHub Actions Guide](https://docs.github.com/en/actions)  
- [Fedora Server Docs](https://docs.fedoraproject.org/en-US/fedora-server/)  
- [Arch Linux Wiki](https://wiki.archlinux.org/title/Main_page)

