<script lang="ts">
	import { onMount } from 'svelte';

	const stats = [
		{ target: 25, suffix: '+', label: 'Yıl Deneyim', icon: `<path d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>` },
		{ target: 50000, suffix: '+', label: 'Mutlu Müşteri', icon: `<path d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"/>` },
		{ target: 100000, suffix: '+', label: 'Aktif Poliçe', icon: `<path d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>` },
		{ target: 12, suffix: '', label: 'Sigorta Şirketi', icon: `<path d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"/>` }
	];

	let values = $state(stats.map(() => 0));
	let counted = false;
	let sectionEl: HTMLElement;

	function formatNumber(n: number): string {
		if (n >= 1000) return (n / 1000).toFixed(0) + '.000';
		return n.toString();
	}

	function animateCounters() {
		if (counted) return;
		counted = true;

		stats.forEach((stat, i) => {
			const duration = 2000;
			const start = performance.now();

			function step(now: number) {
				const elapsed = now - start;
				const progress = Math.min(elapsed / duration, 1);
				const eased = 1 - Math.pow(1 - progress, 3); // easeOutCubic
				values[i] = Math.round(stat.target * eased);
				if (progress < 1) requestAnimationFrame(step);
			}
			requestAnimationFrame(step);
		});
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				if (entries[0].isIntersecting) {
					animateCounters();
					observer.disconnect();
				}
			},
			{ threshold: 0.3 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section id="istatistikler" class="py-20 lg:py-28 bg-gradient-to-br from-teal-800 via-teal-900 to-teal-950 relative overflow-hidden" bind:this={sectionEl}>
	<!-- Background decoration -->
	<div class="absolute inset-0 opacity-10">
		<div class="absolute top-10 left-10 w-40 h-40 border border-white rounded-full"></div>
		<div class="absolute bottom-10 right-10 w-60 h-60 border border-white rounded-full"></div>
		<div class="absolute top-1/2 left-1/3 w-32 h-32 border border-white rounded-full"></div>
	</div>

	<div class="max-w-7xl mx-auto px-6 relative">
		<div class="text-center mb-16" data-aos="fade-up">
			<span class="inline-block text-sm font-semibold text-teal-300 bg-teal-800/50 border border-teal-600/30 px-4 py-1.5 rounded-full mb-4">RAKAMLARLA BİZ</span>
			<h2 class="font-heading font-bold text-3xl sm:text-4xl lg:text-[40px] text-white mb-4">
				Güvenin Rakamsal İfadesi
			</h2>
			<p class="text-teal-200/70 max-w-2xl mx-auto text-lg">
				Yılların deneyimi ve binlerce mutlu müşteri ile sektörde fark yaratıyoruz.
			</p>
		</div>

		<div class="grid grid-cols-2 lg:grid-cols-4 gap-8" data-aos="fade-up" data-aos-delay="200">
			{#each stats as stat, i}
				<div class="text-center">
					<div class="w-16 h-16 mx-auto bg-white/10 rounded-2xl flex items-center justify-center mb-4">
						<svg class="w-8 h-8 text-gold-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.5">
							{@html stat.icon}
						</svg>
					</div>
					<div class="text-4xl lg:text-5xl font-heading font-extrabold text-white mb-2">
						{formatNumber(values[i])}{stat.suffix}
					</div>
					<div class="text-teal-200/70 font-medium">{stat.label}</div>
				</div>
			{/each}
		</div>
	</div>
</section>
