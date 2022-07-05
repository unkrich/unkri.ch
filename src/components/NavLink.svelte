<script>
	import { page } from '$app/stores';
	$: isActive = $page.url.pathname === $$props.href;
	export let href;
</script>

<a
	{href}
	><span class="capsize"><slot /> </span>
</a>
