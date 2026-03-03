<script lang="ts">
	import { onMount } from 'svelte';

	let visible = $state(false);

	onMount(() => {
		setTimeout(() => (visible = true), 100);
	});

	function scrollTo(e: MouseEvent, href: string) {
		e.preventDefault();
		const el = document.querySelector(href);
		if (el) el.scrollIntoView({ behavior: 'smooth' });
	}
</script>

<section id="hero" class="relative min-h-screen flex items-center overflow-hidden bg-gradient-to-br from-white via-teal-50/30 to-white">
	<!-- Animated mesh background -->
	<div class="absolute inset-0 hero-mesh"></div>

	<!-- Decorative shapes -->
	<div class="absolute top-20 right-20 w-72 h-72 shape-circle bg-teal-500"></div>
	<div class="absolute bottom-32 right-40 w-48 h-48 shape-circle bg-gold-400"></div>
	<div class="absolute top-40 left-[60%] w-32 h-32 shape-circle bg-teal-300"></div>

	<!-- Geometric decorations on the right -->
	<div class="hidden lg:block absolute right-0 top-0 w-[45%] h-full">
		<div class="absolute top-[15%] right-[10%] w-64 h-64 border-2 border-teal-200/30 rounded-3xl rotate-12 animate-[float_8s_ease-in-out_infinite]"></div>
		<div class="absolute top-[35%] right-[20%] w-40 h-40 bg-gradient-to-br from-teal-500/10 to-gold-400/10 rounded-2xl -rotate-6 animate-[float_10s_ease-in-out_infinite_-3s]"></div>
		<div class="absolute bottom-[20%] right-[8%] w-52 h-52 border-2 border-gold-400/20 rounded-full animate-[float_12s_ease-in-out_infinite_-5s]"></div>
		<div class="absolute top-[55%] right-[35%] w-20 h-20 bg-teal-500/10 rounded-xl rotate-45 animate-[float_9s_ease-in-out_infinite_-2s]"></div>

		<!-- Dots pattern -->
		<div class="absolute top-[25%] right-[5%] grid grid-cols-5 gap-3 opacity-20">
			{#each Array(25) as _}
				<div class="w-2 h-2 bg-teal-700 rounded-full"></div>
			{/each}
		</div>
	</div>

	<div class="relative max-w-7xl mx-auto px-6 py-20 lg:py-0">
		<div class="lg:w-[55%]">
			<!-- Badge -->
			<div
				class="inline-flex items-center gap-2 bg-teal-50 border border-teal-200 text-teal-800 text-sm font-medium px-4 py-2 rounded-full mb-6 transition-all duration-700 {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}"
			>
				<svg class="w-4 h-4 text-teal-600" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
				Türkiye'nin Güvenilir Sigorta Danışmanı
			</div>

			<!-- Heading -->
			<h1
				class="font-heading font-extrabold text-4xl sm:text-5xl lg:text-[56px] leading-tight text-charcoal-800 mb-6 transition-all duration-700 delay-150 {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}"
			>
				Ailenizi ve Geleceğinizi
				<span class="text-gold-gradient">Güvence</span> Altına Alın
			</h1>

			<!-- Subtitle -->
			<p
				class="text-lg text-charcoal-500 leading-relaxed mb-8 max-w-xl transition-all duration-700 delay-300 {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}"
			>
				12 farklı sigorta şirketinin en uygun tekliflerini karşılaştırıyor,
				size özel çözümler sunuyoruz. Bağımsız danışmanlık avantajıyla
				tasarruf edin.
			</p>

			<!-- CTA Buttons -->
			<div
				class="flex flex-col sm:flex-row gap-4 mb-12 transition-all duration-700 delay-[450ms] {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}"
			>
				<a
					href="#iletisim"
					onclick={(e) => scrollTo(e, '#iletisim')}
					class="inline-flex items-center justify-center gap-2 bg-gold-500 hover:bg-gold-600 text-white font-semibold px-8 py-4 rounded-xl transition-all hover:shadow-xl hover:shadow-gold-500/25 text-base"
				>
					<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>
					Ücretsiz Teklif Al
				</a>
				<a
					href="#sigortalar"
					onclick={(e) => scrollTo(e, '#sigortalar')}
					class="inline-flex items-center justify-center gap-2 border-2 border-teal-800 text-teal-800 hover:bg-teal-800 hover:text-white font-semibold px-8 py-4 rounded-xl transition-all text-base"
				>
					Sigortalarımızı İncele
					<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
				</a>
			</div>

			<!-- Micro stats -->
			<div
				class="flex items-center gap-8 sm:gap-12 transition-all duration-700 delay-[600ms] {visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}"
			>
				<div>
					<div class="text-2xl font-heading font-bold text-teal-800">25+</div>
					<div class="text-sm text-charcoal-500">Yıl Deneyim</div>
				</div>
				<div class="w-px h-10 bg-charcoal-200"></div>
				<div>
					<div class="text-2xl font-heading font-bold text-teal-800">50.000+</div>
					<div class="text-sm text-charcoal-500">Mutlu Müşteri</div>
				</div>
				<div class="w-px h-10 bg-charcoal-200"></div>
				<div>
					<div class="text-2xl font-heading font-bold text-teal-800">12</div>
					<div class="text-sm text-charcoal-500">Sigorta Şirketi</div>
				</div>
			</div>
		</div>
	</div>
</section>
