<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<svelte:head>
	<title>HDM Sigorta - Güvenilir Sigorta Danışmanınız</title>
</svelte:head>

{@render children()}
