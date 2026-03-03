<script lang="ts">
	import { onMount } from 'svelte';

	const partners = [
		{ name: 'Anadolu Sigorta', color: '#003DA5' },
		{ name: 'Allianz', color: '#003781' },
		{ name: 'MAPFRE', color: '#DA291C' },
		{ name: 'AXA', color: '#00008f' },
		{ name: 'HDI', color: '#006341' },
		{ name: 'Zurich', color: '#2167AE' },
		{ name: 'Sompo', color: '#EC6C00' },
		{ name: 'Groupama', color: '#00A651' }
	];

	let swiperEl: HTMLElement;

	onMount(async () => {
		const { Swiper } = await import('swiper');
		const { Autoplay } = await import('swiper/modules');

		new Swiper(swiperEl as any, {
			modules: [Autoplay],
			slidesPerView: 2,
			spaceBetween: 24,
			loop: true,
			speed: 3000,
			autoplay: {
				delay: 0,
				disableOnInteraction: false
			},
			breakpoints: {
				640: { slidesPerView: 3 },
				768: { slidesPerView: 4 },
				1024: { slidesPerView: 5 },
				1280: { slidesPerView: 6 }
			}
		});
	});
</script>

<section class="py-16 lg:py-20 bg-white border-y border-charcoal-100">
	<div class="max-w-7xl mx-auto px-6">
		<div class="text-center mb-12" data-aos="fade-up">
			<span class="inline-block text-sm font-semibold text-teal-700 bg-teal-50 px-4 py-1.5 rounded-full mb-4">İŞ ORTAKLARIMIZ</span>
			<h2 class="font-heading font-bold text-3xl sm:text-4xl text-charcoal-800">
				Güçlü İş Birlikleri
			</h2>
		</div>

		<!-- Swiper -->
		<div bind:this={swiperEl} class="swiper" data-aos="fade-up" data-aos-delay="100">
			<div class="swiper-wrapper items-center">
				{#each partners as partner}
					<div class="swiper-slide">
						<div class="partner-logo flex items-center justify-center h-24 rounded-xl border border-charcoal-100 bg-charcoal-50/50 px-6 select-none">
							<div class="text-center">
								<div class="text-lg font-heading font-bold" style="color: {partner.color}">{partner.name}</div>
								<div class="text-[10px] text-charcoal-400 mt-1">Sigorta</div>
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</div>
</section>
