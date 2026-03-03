<script lang="ts">
	import { onMount } from 'svelte';

	let scrolled = $state(false);
	let mobileOpen = $state(false);

	const navLinks = [
		{ label: 'Ana Sayfa', href: '#hero' },
		{ label: 'Sigortalarımız', href: '#sigortalar' },
		{ label: 'Hakkımızda', href: '#hakkimizda' },
		{ label: 'İstatistikler', href: '#istatistikler' },
		{ label: 'Yorumlar', href: '#yorumlar' },
		{ label: 'İletişim', href: '#iletisim' }
	];

	function handleScroll() {
		scrolled = window.scrollY > 80;
	}

	function closeMobile() {
		mobileOpen = false;
	}

	function scrollTo(e: MouseEvent, href: string) {
		e.preventDefault();
		closeMobile();
		const el = document.querySelector(href);
		if (el) el.scrollIntoView({ behavior: 'smooth' });
	}

	onMount(() => {
		window.addEventListener('scroll', handleScroll, { passive: true });
		return () => window.removeEventListener('scroll', handleScroll);
	});
</script>

<!-- Top bar -->
<div class="bg-teal-900 text-white/80 text-sm hidden md:block">
	<div class="max-w-7xl mx-auto px-6 py-2 flex justify-between items-center">
		<div class="flex items-center gap-6">
			<a href="tel:+902121234567" class="flex items-center gap-2 hover:text-white transition-colors">
				<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/></svg>
				(0212) 123 45 67
			</a>
			<a href="mailto:info@hdmsigorta.com" class="flex items-center gap-2 hover:text-white transition-colors">
				<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
				info@hdmsigorta.com
			</a>
		</div>
		<div class="text-white/60">
			Pzt - Cuma: 09:00 - 18:00
		</div>
	</div>
</div>

<!-- Main nav -->
<header
	class="sticky top-0 z-50 transition-all duration-300 {scrolled ? 'bg-white/95 backdrop-blur-lg shadow-lg header-compact' : 'bg-white'}"
>
	<div class="max-w-7xl mx-auto px-6 py-3 flex items-center justify-between">
		<!-- Logo -->
		<a href="#hero" onclick={(e) => scrollTo(e, '#hero')} class="flex items-center gap-2 shrink-0">
			<div class="w-10 h-10 bg-teal-800 rounded-xl flex items-center justify-center">
				<span class="text-white font-heading font-bold text-lg">H</span>
			</div>
			<div class="flex flex-col">
				<span class="font-heading font-bold text-xl text-teal-900 leading-tight">HDM</span>
				<span class="text-[10px] text-charcoal-500 tracking-widest uppercase -mt-0.5">SİGORTA</span>
			</div>
		</a>

		<!-- Desktop nav -->
		<nav class="hidden lg:flex items-center gap-8">
			{#each navLinks as link}
				<a
					href={link.href}
					onclick={(e) => scrollTo(e, link.href)}
					class="text-[15px] font-medium text-charcoal-700 hover:text-teal-800 transition-colors relative after:absolute after:bottom-[-4px] after:left-0 after:w-0 after:h-0.5 after:bg-teal-700 after:transition-all hover:after:w-full"
				>
					{link.label}
				</a>
			{/each}
		</nav>

		<!-- CTA + Hamburger -->
		<div class="flex items-center gap-4">
			<a
				href="#iletisim"
				onclick={(e) => scrollTo(e, '#iletisim')}
				class="hidden sm:inline-flex items-center gap-2 bg-gold-500 hover:bg-gold-600 text-white font-semibold text-sm px-5 py-2.5 rounded-xl transition-all hover:shadow-lg hover:shadow-gold-500/25"
			>
				Ücretsiz Teklif Al
			</a>

			<!-- Hamburger -->
			<button
				class="lg:hidden p-2 text-charcoal-700 hover:text-teal-800"
				onclick={() => (mobileOpen = !mobileOpen)}
				aria-label="Menü"
			>
				{#if mobileOpen}
					<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M6 18L18 6M6 6l12 12"/></svg>
				{:else}
					<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M4 6h16M4 12h16M4 18h16"/></svg>
				{/if}
			</button>
		</div>
	</div>

	<!-- Mobile menu -->
	{#if mobileOpen}
		<div class="lg:hidden bg-white border-t border-charcoal-100 shadow-lg">
			<nav class="max-w-7xl mx-auto px-6 py-4 flex flex-col gap-1">
				{#each navLinks as link}
					<a
						href={link.href}
						onclick={(e) => scrollTo(e, link.href)}
						class="py-3 px-4 text-charcoal-700 hover:text-teal-800 hover:bg-teal-50 rounded-lg transition-colors font-medium"
					>
						{link.label}
					</a>
				{/each}
				<a
					href="#iletisim"
					onclick={(e) => scrollTo(e, '#iletisim')}
					class="mt-2 text-center bg-gold-500 hover:bg-gold-600 text-white font-semibold py-3 rounded-xl transition-colors"
				>
					Ücretsiz Teklif Al
				</a>
			</nav>
		</div>
	{/if}
</header>
