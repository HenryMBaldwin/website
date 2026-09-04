<script lang="ts">
	import { page } from '$app/state';
	let { pathname, name } = $props();

	let active = $derived(page.url.pathname.startsWith(pathname));
</script>

<div class="{active ? 'bg-black text-white' : ''} px-1">
	<a href={pathname} aria-current={active}>{name}</a>
</div>
