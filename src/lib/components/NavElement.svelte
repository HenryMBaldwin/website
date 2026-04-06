<script lang="ts">
	import { page } from '$app/state';
	let {pathname, name} = $props(); 

	let active = $derived(pathname === page.url.pathname);
</script>

<div class="{active ? "bg-black text-white": ""} px-1">
<a href="{pathname}" aria-current={page}>{name}</a>
</div>
