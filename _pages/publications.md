---
layout: page
permalink: /publications/
title: research
description: 
nav: true
nav_order: 2
---

<hr class="section-divider">

<h2 style="text-align:center; color: var(--global-theme-color);">
  Work in Progress
</h2>

<hr class="section-divider">

<div class="publications">

{% bibliography --query @*[keywords~=work_in_progress] %}

</div>

<hr class="section-divider">

<h2 style="text-align:center; color: var(--global-theme-color);">
  Course Projects
</h2>

{% bibliography --query @*[keywords~=course_project] %}

<hr class="section-divider">
