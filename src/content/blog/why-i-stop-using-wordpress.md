---
title: Why I stop using WordPress for my personal blog
author: Abid Rakhmansyah
pubDatetime: 2023-12-26T10:11:06.130Z
postSlug: why-i-stop-using-wordpress
featured: false
draft: false
tags:
  - general
description: The reason why I stopped using WordPress for my personal blog and chose Astro.
---

We start with the definition of WordPress. WordPress is a free and open-source content management system (CMS) that allows users to create and manage websites and blogs. It allows you to create and manage content for a blog easily. However, I chose to leave WordPress for my personal blog. So, what is the reason?

In this article, I will list all of my personal reasons why I left WordPress for my personal blog.

## Table of contents

## Introduction

Currently, I use Astro for my personal blog. Previously, I used WordPress for my blog, but I encountered some issues that led me to reconsider using WordPress in the future.

There are several reasons I discovered that influenced my decision to choose Astro for my personal blog (instead of Gatsby/Next.js). In this post, I will refer to Astro as an SSG to be more general.

## Need high resources

The first thing that comes to my mind is that using WordPress for a personal blog can be very expensive. This is because WordPress requires a significant amount of resources. I extracted the minimum requirements from the official WordPress website, and here they are:

- PHP version 7.4 or greater.
- MySQL version 5.7 or greater OR MariaDB version 10.4 or greater.
- HTTPS support

To run a WordPress site, you need to purchase hosting. Although there are some free hosting options available, in my experience, the speed tends to be slow because free hosting doesn't provide high-resource servers to run websites. This, in my opinion, is detrimental for a non-profit website like a personal blog.

Choosing Astro for your personal blog is a good option for starting something inexpensively, as you can use platforms such as Vercel, Netlify, GitHub Pages, or Cloudflare Pages to host your personal blog—all of which are free to use.

## Required MySQL

So, why is using MySQL bad for me? Well, since a personal blog doesn't need to have a lot of database relationships, using WordPress for a personal blog is kind of overkill for me. MySQL is well-suited for complex systems because it's a Relational Database Management System (RDBMS).

A blog only needs some necessary data, such as articles, categories, and tags. Furthermore, your blog won't run if you have a failed connection in your MySQL.

## Need to backup your data regularly

Since WordPress stores the data on the internal server, you need to regularly back up your website data.

I had a terrible experience in the past when I used a VPS for my personal blog (WordPress). Suddenly, all my data disappeared due to issues with the hosting provider. I asked the hosting provider if I could retrieve my old data, but unfortunately, since the server had crashed, my data was permanently lost.

In contrast, when using Astro, your data will be hosted on Git (GitHub, GitLab, Bitbucket, etc.). It will always be there as long as your Git provider is running.

## Too slow

Believe it or not, WordPress is slower compared to SSGs (Static Site Generators). WordPress is a dynamic CMS that generates pages on the fly, while SSGs generate static HTML files during the build process.

WordPress relies on server-side processing to generate pages dynamically. This involves querying the database, executing PHP code, and rendering the HTML on the server each time a page is requested. This process can be resource-intensive, especially as the complexity and size of the website increase.

Furthermore, while WordPress does have caching mechanisms, SSGs inherently have an advantage in terms of caching because they generate static files during the build process.

## Complex & overkill

WordPress is too complex and overkill for use in a personal blog. You need to configure various settings within WordPress to make it work as you want. On the other hand, you are required to use their editor to start writing, which incurs costs on both the client side and server side resources.

## Security

SSGs can be more secure because there is no server-side processing or database interactions during runtime.

Unlike WordPress, which involves server-side processing and database interaction, there are potential vulnerabilities in your site, such as SQL Injection, XSS, etc. By not using WordPress, you reduce the potential attack surface and minimize the risk of security vulnerabilities.

## Conclusion

In the end, it's your personal decision whether you want to use WordPress or not. However, as a developer, I recommend starting with an SSG for a personal blog. Choose WordPress if you plan to have dynamic pages that require complex processing. For a personal blog, WordPress may not be as relevant anymore.

The above is my personal opinion. Feel free to discuss with me in the comment section. Thank you!
