<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { page } from '$app/state';
	import NavElement from '$lib/components/NavElement.svelte';

	let { children } = $props();
	
	function page_active(pathname: string): bool {
		return pathname === page.url.pathname;
	} 
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div class="w-full h-full min-h-screen grid grid-rows-[auto_1fr_auto] bg-white">
	<header>
		<nav class="py-2 px-2 sm:px-10 gap-2 sm:gap-4 flex font-medium sm:text-xl border-b-1">
			
			<NavElement pathname="/" name="home"/>
			•
			<NavElement pathname="/writing" name="writing"/>
		</nav>
	</header>
	<main class="mx-auto w-full py-8 px-2 md:px-0 prose prose-hr:border-gray-400">
		{@render children()}
	</main>
	<footer>
		<div class="border-t-1 text-sm py-2 px-4 text-end"> 
			<p> ©2026 Henry Baldwin </p>
		</div>
	</footer>
</div>


