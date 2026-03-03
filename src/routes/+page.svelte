<script lang="ts">
	import { onMount } from 'svelte';
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import Services from '$lib/components/Services.svelte';
	import About from '$lib/components/About.svelte';
	import Partners from '$lib/components/Partners.svelte';
	import Stats from '$lib/components/Stats.svelte';
	import Testimonials from '$lib/components/Testimonials.svelte';
	import ContactForm from '$lib/components/ContactForm.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import FloatingElements from '$lib/components/FloatingElements.svelte';

	onMount(async () => {
		const AOS = (await import('aos')).default;
		await import('aos/dist/aos.css');
		AOS.init({
			duration: 700,
			once: true,
			offset: 80,
			easing: 'ease-out-cubic'
		});
	});
</script>

<Header />
<main>
	<Hero />
	<Services />
	<About />
	<Partners />
	<Stats />
	<Testimonials />
	<ContactForm />
</main>
<Footer />
<FloatingElements />
