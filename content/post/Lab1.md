---
title: "Lab Homework 1: Setup Blog"
slug: "lab1"
url: "/post/lab1/"
date: 2025-12-01
weight: 5
author: Yan Zhuang
draft: false
---

## Introduction

In this blog post, I reflect on my experience as a student building and deploying my first blog using **Hugo** and **GitHub Pages**. Although Hugo is a static site generator, the process taught me a lot about project structure, configuration, and deployment workflows.

---

## How I Approached This Task

I approached this task step by step. First, I focused on installing Hugo correctly and making sure it worked locally. After that, I created a new Hugo site and selected an existing theme instead of designing everything from scratch.

Once the site worked locally, I followed the deployment method introduced in the course slides, which uses GitHub Pages with the `docs/` folder.

---

## Problems I Encountered and How I Overcame Them

### Downloading the Wrong Hugo Package

One of the first problems I encountered was downloading the **source code** version of Hugo instead of the precompiled Windows executable. This resulted in a folder full of files but no `hugo.exe`, so I could not run Hugo from the command line.

I solved this by downloading the correct file named similar to `hugo_extended_xxx_windows-amd64.zip` from the Hugo releases page and adding it to my system PATH.

---

### Theme Configuration Errors

Another issue occurred when Hugo could not find the selected theme. This happened because the theme folder name did not exactly match the theme name specified in `hugo.toml`.

Renaming the theme folder so that it matched the configuration file resolved the error. This helped me understand how strictly Hugo depends on correct naming and directory structure.

---

## What I Learned

The most important lesson from this task was understanding Hugo’s content structure. Each page on the website corresponds to a file inside the `content/` directory, while navigation menus only link to those pages.

I also learned that small configuration details, such as folder names and URL paths, can have a significant impact on whether a site works correctly after deployment.

---

## Conclusion

Overall, building and deploying a Hugo blog was a valuable learning experience. The process improved my understanding of static site generation, configuration management, and GitHub Pages deployment. For students attempting a similar project, I strongly recommend testing everything locally and paying close attention to configuration details.