---
title: "旅行 Travel"
permalink: /travel/
layout: single
author_profile: false
---

<div class="works-filter">
<button class="is-active" data-filter="all">全部</button>
{%- assign countries = site.posts | map: "country" | compact | uniq | sort -%}
{%- for c in countries -%}
<button data-filter="{{ c }}">{{ c }}</button>
{%- endfor -%}
</div>

<div class="works-grid">
{%- for post in site.posts -%}
{%- if post.cover -%}
<a class="work" href="{{ post.url | relative_url }}" data-country="{{ post.country }}">
<img src="{{ post.cover | relative_url }}" alt="{{ post.title }}" loading="lazy">
<span class="work__cover"><span class="work__title">{{ post.title }}</span><span class="work__meta">{{ post.period }}</span></span>
</a>
{%- endif -%}
{%- endfor -%}
</div>

<div id="curtain"></div>

<script>
document.querySelectorAll('.works-filter button').forEach(function (btn) {
  btn.addEventListener('click', function () {
    document.querySelectorAll('.works-filter button').forEach(function (b) {
      b.classList.toggle('is-active', b === btn);
    });
    var f = btn.dataset.filter;
    document.querySelectorAll('.work').forEach(function (w) {
      w.classList.toggle('is-hidden', f !== 'all' && w.dataset.country !== f);
    });
  });
});

var curtain = document.getElementById('curtain');
document.querySelectorAll('.work').forEach(function (a) {
  a.addEventListener('click', function (e) {
    if (e.metaKey || e.ctrlKey || e.shiftKey || e.button !== 0) return;
    e.preventDefault();
    curtain.classList.add('is-on');
    setTimeout(function () { location.href = a.href; }, 650);
  });
});
window.addEventListener('pageshow', function () {
  curtain.classList.remove('is-on');
});
</script>
