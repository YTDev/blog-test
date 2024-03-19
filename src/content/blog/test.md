---
title: test
description: something...
pubDate: 2024-03-18T00:29:17.513Z
heroImage: /uploads/img9.png
---
Decap CMS logo

Search the docs

Docs

Pro HelpNew

Community

Blog

Intro to Decap CMS

Overview

Start With A Template

Releases

Add To Your Site

Basic Steps

1. Install Decap CMS

2. Choosing A Backend

3. Configure Decap CMS

4. Access Your Content

Account Settings

Overview

Git Gateway

Azure

Bitbucket

Gitea / Forgejo

GitHub

GitLab

Test

External OAuth Clients

Working With A Local Git Repository

Configuring your Site

Configuration Options

I18n Support

Media

Cloudinary

Netlify Large Media

Uploadcare

Workflow

Deploy Preview Links

Editorial Workflows

Open Authoring

Collections

Folder Collections

File Collections

Nested Collections (Beta)

Summary String Transformations

Fields

Widgets

Creating Custom Widgets

Dynamic Default Values

Platform Guides

Gatsby

Hugo

Jekyll

NextJS

Nuxt

Middleman

Gridsome

Docusaurus

Customizing Decap CMS

Creating Custom Previews

Custom Formatters

Manual Initialization

Registering To CMS Events

Custom Mount Element

Community

Contributor Guide

Writing Style Guide

Examples

Architecture

 Edit this page

2. Choosing a Backend

Now that you have your Decap CMS files in place and configured, all that's left is to enable authentication. We're using the Netlify platform here because it's one of the quickest ways to get started, but you can learn about other authentication options in the Backends doc.



Setup on Netlify

Netlify offers a built-in authentication service called Identity. In order to use it, connect your site repo with Netlify. Netlify has published a general Step-by-Step Guide for this, along with detailed guides for many popular static site generators, including Jekyll, Hugo, Hexo, Middleman, Gatsby, and more.



Enable Identity and Git Gateway

Netlify's Identity and Git Gateway services allow you to manage CMS admin users for your site without requiring them to have an account with your Git host or commit access on your repo. From your site dashboard on Netlify:



Go to Settings > Identity, and select Enable Identity service.

Under Registration preferences, select Open or Invite only. In most cases, you want only invited users to access your CMS, but if you're just experimenting, you can leave it open for convenience.

If you'd like to allow one-click login with services like Google and GitHub, check the boxes next to the services you'd like to use, under External providers.

Scroll down to Services > Git Gateway, and click Enable Git Gateway. This authenticates with your Git host and generates an API access token. In this case, we're leaving the Roles field blank, which means any logged in user may access the CMS. For information on changing this, check the Netlify Identity documentation.

Add the Netlify Identity Widget

With the backend configured to handle authentication, now you need a frontend interface to connect to it. The open source Netlify Identity Widget is a drop-in widget made for just this purpose. To include the widget in your site, add the following script tag in two places:



<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>

Add this to the <head> of your CMS index page at /admin/index.html, as well as the <head> of your site's main index page. Depending on how your site generator is set up, this may mean you need to add it to the default template, or to a "partial" or "include" template. If you can find where the site stylesheet is linked, that's probably the right place. Alternatively, you can include the script in your site using Netlify's Script Injection feature.



When a user logs in with the Netlify Identity widget, an access token directs to the site homepage. In order to complete the login and get back to the CMS, redirect the user back to the /admin/ path. To do this, add the following script before the closing body tag of your site's main index page:



<script>

  if (window.netlifyIdentity) {

\    window.netlifyIdentity.on("init", (user) => {

\    if (!user) {

\    window.netlifyIdentity.on("login", () => {

\    document.location.href = "/admin/";

\    });

\    }

\    });

  }

</script>

Note: This example script requires modern JavaScript and does not work on IE11. For legacy browser support, use function expressions (function () {}) in place of the arrow functions (() => {}), or use a transpiler such as Babel.



Previous

1. Install Decap CMS

Next

3. Configure Decap CMS

You blocked an ad that keeps this project alive

Please consider supporting Decap by donating on Open Collective or sponsoring on GitHub.



GitHub

Distributed under MIT License · Maintained by PM · Code of Conduct



Navigated to 2. Choosing a Backend

Join us on



Discord
