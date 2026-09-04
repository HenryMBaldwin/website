<script lang="ts">
	import './layout.css';
	import freak from '$lib/assets/freak-icon-invert.png';
	import { page } from '$app/state';
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';
	import NavElement from '$lib/components/NavElement.svelte';

	let { children } = $props();

	function page_active(pathname: string): boolean {
		return pathname === page.url.pathname;
	}

	let dark = $state(false);
	let ready = $state(false);

	onMount(() => {
		dark = localStorage.getItem('dark') === 'true';
		ready = true;
	});

	$effect(() => {
		if (browser) {
			localStorage.setItem('dark', String(dark));
		}
	});
</script>

<svelte:head><link rel="icon" href={freak} /></svelte:head>

{#if ready}
	<div
		class="grid h-full min-h-screen w-full grid-rows-[auto_1fr_auto] bg-white {dark
			? 'invert [&_img]:invert'
			: ''}"
	>
		<header
			class="grid grid-cols-2 border-b-1 px-2 py-2 font-medium sm:gap-4 sm:px-10 sm:text-xl"
		>
			<nav class="flex gap-2">
				<NavElement pathname="/home" name="home" />
				•
				<NavElement pathname="/writing" name="writing" />
				•
				<NavElement pathname="/poetry" name="poetry" />
			</nav>
			<button
				class="sm: text-md justify-self-end"
				onclick={() => (dark = !dark)}
				>{dark ? 'dark' : 'light'}
			</button>
		</header>
		<main
			class="mx-auto prose w-full px-2 py-8 md:px-0 prose-hr:border-gray-400"
		>
			{@render children()}
		</main>
		<footer>
			<div class="border-t-1 px-4 py-2 text-end text-sm">
				<p>©2026 Henry Baldwin</p>
			</div>
		</footer>
	</div>
{/if}
