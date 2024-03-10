---
title: "Fixing Github Build Errors for Jekyll-based Website"
categories:
  - Site Documentation
tags:
last_modified_at: 2023-06-29T14:25:52-05:00
comments: false
layout: page
---
Whilst having the website run fine locally is great, getting it to deploy properly would be even better.

{% raw %}
## Introduction

When working with Jekyll-based websites on GitHub, encountering build errors can be frustrating. In this guide, we'll address a common issue faced by users when deploying Jekyll websites on GitHub Pages. We'll walk through the problem, potential causes, and step-by-step solutions to get your website up and running smoothly.

## The Problem: Build Errors on GitHub Pages

Users often encounter build errors when deploying Jekyll-based websites on GitHub Pages. These errors can manifest in various ways, hindering the successful deployment of your site. One specific scenario is the inability to find a specified Jekyll theme, leading to broken builds and deployment.

## Identifying the Issue

Upon inspecting the GitHub Actions deployment logs, you may encounter error messages such as:

- **Error**: The jekyll-theme-basically-basic theme could not be found.
- **Warning**: github-pages can't satisfy your Gemfile's dependencies.

These errors indicate that GitHub Pages is struggling to locate the specified Jekyll theme, which is crucial for the proper functioning of your website.

## Possible Solutions

### 1. Check Your Gemfile

If your Gemfile specifies a Jekyll version that differs from what GitHub Pages supports, it can lead to compatibility issues. GitHub Pages might utilize an older Jekyll version than what's specified in your Gemfile.

### 2. Theme Configuration

If you've specified a Jekyll theme in your `_config.yml` file, like `theme: jekyll-theme-basically-basic`, GitHub Pages might encounter difficulties locating it. This is particularly true if you cloned a theme repository into your project.

### 3. Removing Unnecessary Files

Sometimes, your Gemfile might contain only the Jekyll version and no additional dependencies. In such cases, you can safely remove the Gemfile to prevent any interference with GitHub Pages' deployment process.

### 4. Manual Build Initiation

Initiating a manual build on GitHub Pages might help resolve issues caused by failed automatic builds. This can be done through the GitHub Actions interface.

## Resolving the Issue

Following these steps should help you overcome the GitHub build errors for your Jekyll-based website:

1. Check and adjust your Gemfile to ensure compatibility with GitHub Pages' supported Jekyll version.
2. If you cloned a theme repository, remove any theme-related configuration from your `_config.yml` file.
3. Consider removing unnecessary files like the Gemfile if it contains minimal information.
4. Initiate a manual build on GitHub Actions to trigger the deployment process and check for any errors.

## Conclusion

Deploying a Jekyll-based website on GitHub Pages can sometimes lead to build errors that hinder your site's availability. By understanding the underlying causes and implementing the suggested solutions, you can successfully troubleshoot and overcome these challenges. With your GitHub-hosted Jekyll website now up and running, you can focus on showcasing your content without being hindered by deployment issues.
{% endraw %}