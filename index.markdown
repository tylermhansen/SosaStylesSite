---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Home
description: "Bridal hair in Standish, Maine — Timeless artistry for the modern bride."
---
 
<section id="home" class="relative w-full h-[70vh] lg:h-[80vh] bg-cover bg-center" style="background-image: url('{{ site.hero_image }}')">
	<div class="absolute inset-0" style="background: linear-gradient(rgba(0,0,0,0.25), rgba(0,0,0,0.25));"></div>
	<div class="relative z-10 flex items-center justify-center h-full">
		<div class="text-center max-w-3xl px-6">
			<h1 class="font-heading text-white text-4xl sm:text-5xl md:text-6xl tracking-tight">Timeless Artistry for the Modern Bride</h1>
			<p class="mt-4 text-sm text-white/90">Sosa Studios — Bridal Hair in Standish, Maine</p>
			<a href="/#contact" class="mt-8 inline-block bg-[color:var(--color-champagne)] text-[color:var(--color-charcoal)] font-medium py-3 px-6 rounded-md shadow-sm">Book a Consultation</a>
		</div>
	</div>
</section>

<section class="py-16">
	<div class="container mx-auto px-6 text-center">
		<p class="font-heading text-2xl md:text-3xl text-[color:var(--color-charcoal)]">Timeless Artistry for the Modern Bride</p>
		<p class="mt-4 max-w-2xl mx-auto text-gray-700">We create editorial, refined bridal hairstyles that photograph beautifully and last all day.</p>
	</div>
</section>

<section id="featured" class="py-12 bg-white">
	<div class="container mx-auto px-6">
		<h2 class="font-heading text-2xl mb-6">Featured Work</h2>
		<div class="relative">
			<!-- Carousel container -->
			<div class="overflow-hidden">
				   <div id="carousel" class="flex gap-6 transition-transform duration-500">
					   {% for item in site.data.portfolio.items %}
					   <figure class="w-full sm:w-1/2 lg:w-1/3 flex-shrink-0 overflow-hidden rounded-lg bg-white shadow-sm">
						   <button class="portfolio-item w-full text-left" type="button" data-portfolio-index="{{ forloop.index0 }}" data-images='{{ item.images | jsonify }}' data-title="{{ item.title }}" data-description="{{ item.description }}" data-package="{{ item.package }}" data-date="{{ item.date }}">
							   <div class="w-full h-64 overflow-hidden">
								   <img src="{{ item.src }}" alt="{{ item.alt }}" class="w-full h-full object-cover" loading="lazy">
							   </div>
							   {% if item.title %}<figcaption class="p-4 text-sm text-gray-700">{{ item.title }}</figcaption>{% endif %}
						   </button>
					   </figure>
					   {% endfor %}
				</div>
			</div>

			<!-- Carousel controls -->
			<button id="carousel-prev" class="absolute left-0 top-1/3 -translate-y-1/2 -ml-6 sm:-ml-8 text-charcoal hover:bg-gray-200 rounded-full p-2 z-10">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" /></svg>
			</button>
			<button id="carousel-next" class="absolute right-0 top-1/3 -translate-y-1/2 -mr-6 sm:-mr-8 text-charcoal hover:bg-gray-200 rounded-full p-2 z-10">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" /></svg>
			</button>

			<!-- Indicator dots -->
			<div id="carousel-dots" class="flex justify-center gap-2 mt-6"></div>
		</div>
	</div>
</section>

<script>
  // Portfolio carousel
  (function(){
    const carousel = document.getElementById('carousel');
    const prevBtn = document.getElementById('carousel-prev');
    const nextBtn = document.getElementById('carousel-next');
    const dotsContainer = document.getElementById('carousel-dots');
    const items = document.querySelectorAll('#carousel > figure');
    
    const itemsPerView = window.innerWidth < 768 ? 1 : (window.innerWidth < 1024 ? 2 : 3);
    const totalSlides = Math.ceil(items.length / itemsPerView);
    let currentSlide = 0;
    let autoPlayTimer = null;

    function createDots(){
      dotsContainer.innerHTML = '';
      for(let i = 0; i < totalSlides; i++){
        const dot = document.createElement('button');
        dot.className = `w-2 h-2 rounded-full transition-colors ${i === currentSlide ? 'bg-[color:var(--color-charcoal)]' : 'bg-gray-300'}`;
        dot.addEventListener('click', ()=> goToSlide(i));
        dotsContainer.appendChild(dot);
      }
    }

    function goToSlide(n){
      currentSlide = (n + totalSlides) % totalSlides;
      const offset = currentSlide * -100 / itemsPerView;
      carousel.style.transform = `translateX(${offset}%)`;
      createDots();
      resetAutoPlay();
    }

    function nextSlide(){ goToSlide(currentSlide + 1); }
    function prevSlide(){ goToSlide(currentSlide - 1); }

    function startAutoPlay(){
      autoPlayTimer = setInterval(nextSlide, 5000);
    }

    function stopAutoPlay(){
      clearInterval(autoPlayTimer);
    }

    function resetAutoPlay(){
      stopAutoPlay();
      startAutoPlay();
    }

    // Expose start/stop for lightbox coordination
    window.carouselAutoPlayStart = startAutoPlay;
    window.carouselAutoPlayStop = stopAutoPlay;

    prevBtn.addEventListener('click', prevSlide);
    nextBtn.addEventListener('click', nextSlide);
    
    createDots();
    startAutoPlay();
  })();
</script>

<section id="about" class="py-20 bg-[color:var(--color-cream)]">
	<div class="container mx-auto px-6 max-w-3xl">
		<h2 class="font-heading text-3xl mb-4">About</h2>
		<p class="text-gray-700">Every bride deserves a stylist who is as invested in the vision as they are. I’m Nadia, but most people call me Lulu. After graduating from Lowell Academy, I brought my shears home to Standish, Maine, where I’ve been crafting custom looks at Tangles Hair Salon. I am a dual-licensed stylist in Maine and Massachusetts, which means I’m always on the move, bringing luxury bridal hair to women across New England. For me, it’s about more than just the perfect curl; it’s about the confidence you feel when you step into your dress. I can’t wait to help you find your "Sosa Studio" look.</p>
	</div>
</section>

<section id="investment" class="py-20 bg-white">
	<div class="container mx-auto px-6 max-w-3xl">
		<h2 class="font-heading text-3xl mb-6">Investment</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 gap-6">
			<div class="p-6 border border-gray-200 rounded-md bg-white">
				<h3 class="font-heading text-xl mb-2">Classic</h3>
				<p class="mb-4 text-gray-700">Starting at $200 — Trial (optional) + Bridal styling for ceremony day. Ideal for intimate ceremonies and elopements.</p>
				<ul class="text-sm text-gray-600 space-y-1">
					<li>✓ Consultation</li>
					<li>✓ On-site styling</li>
					<li>✓ Light touch-ups</li>
				</ul>
			</div>

			<div class="p-6 border border-gray-200 rounded-md bg-white">
				<h3 class="font-heading text-xl mb-2">Editorial</h3>
				<p class="mb-4 text-gray-700">Starting at $350 — Includes trial session and full-day support. Perfect for editorial looks and multi-person styling.</p>
				<ul class="text-sm text-gray-600 space-y-1">
					<li>✓ Trial session</li>
					<li>✓ Bridal + party styling</li>
					<li>✓ Travel & on-site support</li>
				</ul>
			</div>
		</div>

		<p class="mt-6 text-sm text-gray-600">All packages are examples. For an accurate quote, please inquire with your wedding date, guest count, and location.</p>
	</div>
</section>

<section id="day-of" class="py-20 bg-[color:var(--color-cream)]">
	<div class="container mx-auto px-6 max-w-3xl">
		<h2 class="font-heading text-3xl mb-4">Day Of — Example Timeline</h2>

		<ol class="list-decimal ml-6 space-y-4 text-gray-700">
			<li><strong>8:00 AM</strong> — Arrival and setup at venue or preparation location.</li>
			<li><strong>8:30 AM</strong> — Begin bridal party styling (hair only) — bridesmaids and family.</li>
			<li><strong>10:30 AM</strong> — Bridal trial/style touch and veil placement.</li>
			<li><strong>11:00 AM</strong> — Final checks, touch-ups, and photography prep.</li>
			<li><strong>12:00 PM</strong> — Ceremony styling complete; on-call for touch-ups.</li>
		</ol>

		<p class="mt-6 text-sm text-gray-600">This timeline is illustrative. Exact scheduling depends on guest count, travel time, and services booked.</p>
	</div>
</section>

<section id="contact" class="py-20 bg-white">
	<div class="container mx-auto px-6 max-w-2xl">
		<h2 class="font-heading text-3xl mb-4">Contact</h2>
		<p class="mb-6 text-gray-700">For inquiries and bookings, please email <a href="mailto:{{ site.social.email }}" class="underline hover:no-underline">{{ site.social.email }}</a> or use the details below to schedule a consultation.</p>

		<div class="bg-[color:var(--color-cream)] p-6 rounded-md shadow-sm border border-gray-200">
			<p class="mb-2"><strong>Location:</strong> {{ site.brand.location }}</p>
			<p class="mb-4"><strong>Studio:</strong> Sosa Studios</p>

			<p class="mb-4 text-sm text-gray-700">To request availability, please send a message with your wedding date, venue, and style inspiration. For faster response, include images if you have them.</p>

			<a href="mailto:{{ site.social.email }}?subject=Consultation%20Request" class="inline-block bg-[color:var(--color-champagne)] text-[color:var(--color-charcoal)] font-medium py-2 px-4 rounded hover:opacity-90 transition">Email to Book</a>
		</div>
	</div>
</section>

<script>
	window.portfolioData = {{ site.data.portfolio.items | jsonify }};
</script>
