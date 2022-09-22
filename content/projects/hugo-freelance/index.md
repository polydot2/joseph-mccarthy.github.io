---
title: "Hugo Freelance"
date: 2022-03-01T17:23:53Z
draft: false
sidebar: false
tags: [Bootstrap, Freelancer, Hugo, Theme]
hero: "hero.png"
summary: I wanted to use Hugo and I wanted Bootstrap Freelance. So here it is.
images: "hero.png"

---
<div class="text-center m-2">

[![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_hugo-bootstrap-freelancer-template?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://sonarcloud.io/project/overview?id=joseph-mccarthy_hugo-bootstrap-freelancer-template)
[![GitHub](https://img.shields.io/github/license/joseph-mccarthy/hugo-bootstrap-freelancer-template?style=for-the-badge)](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template/blob/main/LICENSE)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/joseph-mccarthy/hugo-bootstrap-freelancer-template?color=green&style=for-the-badge)](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template/releases/latest)
[![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/hugo-bootstrap-freelancer-template.svg?style=for-the-badge)](https://wakatime.com/badge/github/joseph-mccarthy/hugo-bootstrap-freelancer-template)

</div>

This repository contains a [Hugo](https://github.com/gohugoio) theme that is based on the [Bootstrap](https://getbootstrap.com/) Freelancer template. I created this Hugo theme as I have always liked the [Freelancer](https://github.com/StartBootstrap/startbootstrap-freelancer) Bootstrap template, and my preference for Hugo for static site generation made it a no brainer to me. As the origional Freelancer theme was a single page template, I have used some creative licence when it comes to the post listing pages, and content pages. If you have any suggestions on how it can be made better, please commit. To see an example of a site running it? Well you are as my site has been built with this template. You can also see the repository for the Hugo/Freelance theme [here.](https://github.com/joseph-mccarthy/hugo-bootstrap-freelancer-template)

## How To Use

---
You can use this theme like you would with any Hugo theme. The generally accepted way of using themes is to install them as a git sub module so you're able to keep them upto date with the theme repository.

<script src="https://gist.github.com/joseph-mccarthy/71d1a23c791be31d27b72f4f4f2c5f4d.js?file=set-theme.sh"></script>

This theme also comes with it's own default content type, and should be used also along with the idea of bundles. Here is an example command on how to use the default content type

<script src="https://gist.github.com/joseph-mccarthy/71d1a23c791be31d27b72f4f4f2c5f4d.js?file=add-post.sh"></script>

This content type has some font matter that you'll be able to make use of as it's using bundles. There is a field named "hero" which would be the path to the banner image of the post, this image is also used in the post listing pages. The "sidebar" field states if to show the post as full width or with the meta sidebar which will show related posts and last 5 publised posts.

There are also some extra paramters that should be added to your config.toml in order to use the theme to it's full.

<script src="https://gist.github.com/joseph-mccarthy/71d1a23c791be31d27b72f4f4f2c5f4d.js?file=config.toml"></script>

There are also some assumptions made on the content structure for this theme. I have created this with the idea of two areas __posts__ and __projects__ which will drive the menu, home page and content listing areas.

## References

- [Hugo](https://github.com/gohugoio)
- [Bootstrap](https://getbootstrap.com/)
- [Bootstrap Freelancer](https://github.com/StartBootstrap/startbootstrap-freelancer)
- [Bootstrap Forms](https://startbootstrap.com/solution/contact-forms)
