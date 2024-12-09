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

	/* Popup Styles */
	.popup {
	  display: none;
	  position: fixed;
	  top: 0;
	  left: 0;
	  width: 100%;
	  height: 100%;
	  background: rgba(0, 0, 0, 0.8);
	  justify-content: center;
	  align-items: center;
	  z-index: 1000;
	  flex-direction: column; /* Stack image and caption vertically */
	}

	.popup.active {
	  display: flex;
	}

	.popup img {
	  max-width: 90%;
	  max-height: 80%;
	  margin-bottom: 16px; 
	  width: auto;
	}

	.popup .caption-container {
	  width: 35%; 
	  max-width: 35%; 
	  padding: 0 10px;
	}

	.popup .caption {
	  color: #fff;
	  font-size: 18px;
	  text-align: center; 
	  word-wrap: break-word;
	  white-space: normal; 
	}

	.popup .close {
	  position: absolute;
	  top: 20px;
	  right: 20px;
	  color: #fff;
	  font-size: 24px;
	  cursor: pointer;
	  background: none;
	  border: none;
	}
</style>



<!-- Popup -->
<div class="popup" id="imagePopup">
  <button class="close" id="popupClose">&times;</button>
  <img id="popupImage" src="" alt="">
  <div class="caption-container">
    <div class="caption" id="popupCaption"></div>
  </div>
</div>

<script>
  const galleryImages = document.querySelectorAll('.gallery .image img');
  const popup = document.getElementById('imagePopup');
  const popupImage = document.getElementById('popupImage');
  const popupCaption = document.getElementById('popupCaption');
  const popupClose = document.getElementById('popupClose');

  // Open popup
  galleryImages.forEach(image => {
    image.addEventListener('click', () => {
      popupImage.src = image.src;
      popupCaption.textContent = image.getAttribute('data-caption');
      popup.classList.add('active');
    });
  });

  // Close popup
  popupClose.addEventListener('click', () => {
    popup.classList.remove('active');
    popupImage.src = '';
    popupCaption.textContent = '';
  });

  // Close popup when clicking outside the image
  popup.addEventListener('click', (e) => {
    if (e.target === popup) {
      popupClose.click();
    }
  });
</script>

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