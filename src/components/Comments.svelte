<script>
	/** @type {import('$lib/types').GHMetadata} */
	export let ghMetadata;
	let data = [];
	import { onMount } from 'svelte';
	onMount(async () => {
		data = await (await fetch(ghMetadata.commentsUrl)).json();
	});
	import Comment from './Comment.svelte';
</script>

<div class="prose mb-8 w-full dark:prose-invert">
	{#each data as comment}
		<Comment {comment} />
	{/each}
</div>
<a
	href={`${ghMetadata.issueUrl}#issuecomment-new`}
	rel="external"
	target="_blank"
	class="flex justify-center border-y border-blue-700 p-4 no-underline hover:text-yellow-700 dark:hover:text-yellow-200 sm:inline sm:rounded-xl sm:border-x"
>
	Leave a new comment!
</a>