---
title: "Hugo Freelance Devlog"
date: 2022-09-16T20:02:03+01:00
draft: true
sidebar: true
tags: [Bootstrap, Freelancer, Hugo, Developer Log,Project]
hero: "hero.png"
summary: "Developer Log for Bootstrap Freelancer Theme for Hugo"
---

<div class="text-center m-2">

[![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_hugo-bootstrap-freelancer-template?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://sonarcloud.io/project/overview?id=joseph-mccarthy_hugo-bootstrap-freelancer-template)
[![GitHub](https://img.shields.io/github/license/joseph-mccarthy/hugo-bootstrap-freelancer-template?style=for-the-badge)](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template/blob/main/LICENSE)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/joseph-mccarthy/hugo-bootstrap-freelancer-template?color=green&style=for-the-badge)](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template/releases/latest)
[![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/hugo-bootstrap-freelancer-template.svg?style=for-the-badge)](https://wakatime.com/badge/github/joseph-mccarthy/hugo-bootstrap-freelancer-template)

</div>

This Developer Log has been created after a lot of development has taken place, as I wasn't keeping developer logs when I started this project of a [Hugo](https://github.com/gohugoio) theme that is based on the [Bootstrap](https://getbootstrap.com/) Freelancer template. I created this Hugo theme as I have always liked the [Freelancer](https://github.com/StartBootstrap/startbootstrap-freelancer) Bootstrap template, and my preference for Hugo for static site generation made it a no brainer to me. 

As the origional Freelancer theme was a single page template, I have used some creative licence when it comes to the post listing pages, and content pages. If you have any suggestions on how it can be made better, please commit. To see an example of a site running it? Well you are as my site has been built with this template. You can also see the repository for the Hugo/Freelance theme [here.](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template). As you can see that this site is actually running the theme, so yes I'm eating my own dog food.

----

## 16/09/2022

A new version of the Freelancer Bootstrap Hugo theme has been released today. This can be found on [GitHub](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template/releases/tag/v1.0.2). This version has a few issues address. Firstly after performing a Hugo upgrade, found that __{.URL}__ is no longer supported and was required to change this field to __{.Permalink}__. Secondly I have address some sonar concerns that were raised. Mostly to do with duplications within the CSS and hash checks on the CDN downloads. 

