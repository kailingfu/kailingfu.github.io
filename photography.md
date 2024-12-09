---
layout: page
title: Photography
description: People, places, things
image: assets/images/photography.png
nav-menu: true
---

<header class="major">
  <h1>Photography</h1>
</header>

<style>
    .gallery {
      display: flex;
      flex-wrap: wrap;
    }
    .gallery .image {
      display: flex;
      justify-content: center;
      align-items: center;
      flex: 1 1 calc(33%);
      max-width: calc(33%);
      box-sizing: border-box;
	  height: 250px;
	  overflow: hidden;
    }
    .gallery .image img {
      width: 100%;
      height: auto;
	  object-fit: cover;
      display: block;
      cursor: pointer;
      transition: transform 0.2s ease; /* Optional hover effect */
    }
    .gallery .image img:hover {
      transform: scale(1.05);
    }
</style>

<div class="gallery">
  {% assign gallery_folder = "assets/images/gallery" %}
  {% for image in site.static_files %}
    {% if image.path contains gallery_folder %}
      <div class="image">
        <img src="{{ image.path | relative_url }}" alt="{{ image.name }}" data-caption="{{ image.name }}">
      </div>
    {% endif %}
  {% endfor %}
</div>