<script context="module">
	import {
		SITE_TITLE
	} from '$lib/siteConfig';

	// export const prerender = true; // turned off so it refreshes quickly
	export async function load({ params, fetch }) {
		const res = await fetch(`/api/listContent.json`);
		// alternate strategy https://www.davidwparker.com/posts/how-to-make-an-rss-feed-in-sveltekit
		// Object.entries(import.meta.glob('./*.md')).map(async ([path, page]) => {
		if (res.status > 400) {
			return {
				status: res.status,
				error: await res.text()
			};
		}

		/** @type {import('$lib/types').ContentItem[]} */
		const items = await res.json();
		return {
			props: { items },
			cache: {
				maxage: 60 // 1 minute
			}
		};
	}

	import {
		SITE_URL,
		REPO_URL,
		SITE_DESCRIPTION,
		DEFAULT_OG_IMAGE,
		MY_TWITTER_HANDLE
	} from '$lib/siteConfig';
	export const prerender = true; // index page is most visited, lets prerender
</script>

<script>
	import Newsletter from '../components/Newsletter.svelte';
	import FeatureCard from '../components/FeatureCard.svelte';

	export let list;

	// technically this is a slighlty different type because doesnt have 'content' but we'll let it slide
	/** @type {import('$lib/types').ContentItem[]} */
	export let items;

	let inputEl;
	function focusSearch(e) {
		if (e.key === '/' && inputEl) inputEl.select();
	}

	let isTruncated = items.length > 20;
	let search;
	$: list = items
		.filter((item) => {
			if (search) {
				return item.title.toLowerCase().includes(search.toLowerCase());
			}
			return true;
		})
		.slice(0, isTruncated ? 2 : items.length);

</script>

<svelte:head>
	<title>{SITE_TITLE}</title>
	<link rel="canonical" href={SITE_URL} />
	<link rel="alternate" type="application/rss+xml" href={SITE_URL + '/api/rss.xml'} />
	<meta property="og:url" content={SITE_URL} />
	<meta property="og:type" content="article" />
	<meta property="og:title" content={SITE_TITLE} />
	<meta name="Description" content={SITE_DESCRIPTION} />
	<meta property="og:description" content={SITE_DESCRIPTION} />
	<meta property="og:image" content={DEFAULT_OG_IMAGE} />
	<meta name="twitter:card" content="summary" />
	<meta name="twitter:creator" content={'@' + MY_TWITTER_HANDLE} />
	<meta name="twitter:title" content={SITE_TITLE} />
	<meta name="twitter:description" content={SITE_DESCRIPTION} />
	<meta name="twitter:image" content={DEFAULT_OG_IMAGE} />
</svelte:head>

<div>
	<article class="hero">
	    <header>
	      <div class="container">
	        <div class="flex-content">
	          <div>
	            <h1>Hey, I'm Kevin Unkrich.</h1>
	            <p class="subtitle small">
	              I'm a founder and software engineer living in San Francisco.
	            </p>
	          </div>
	          <!--
	          <img src={DEFAULT_OG_IMAGE} alt="Me" class="main-image" />
	          -->
	        </div>
	      </div>
	    </header>


        <div class="container">
        	<!-- Featured Posts -->
					<!-- <section class="mb-16 w-full">
						<div class="flex flex-col gap-6 md:flex-row">
							<FeatureCard title="Welcome to unkri.ch!" href="/welcome" stringData="Jan 2022" />
							<FeatureCard
								title="Example Title"
								href="/example-title"
								stringData="Jan 2022"
							/>
							<FeatureCard title="HTML Ipsum demo" href="/moo" stringData="Jan 2022" />
						</div>
					</section>
					-->


        	<!-- Latest Articles -->
				  <h2 class="main-header">
				    <span>Latest Articles</span>
				    <a href="/blog">View All</a>
				  </h2>
				  <div class="posts">
				  	{#each list as item}
					    <a class="post" href="{item.slug}">
					      <span class="flex" style="align-items: center;">
					        <h3>{item.title}</h3>
					        <span class="new-badge"></span>
					      </span>
					      <div>
					        <time>{new Date(item.date).toISOString().slice(5, 10)}</time>
					      </div>
					    </a>
				    {/each}
				  </div>

<!--
          <h2 class="main-header">Newsletter</h2>
          <div class="flex-content">
            <p>
              Subscribe to the newsletter to get my latest content by email. Not
              on any set schedule. Unsubscribe anytime.
            </p>
          </div>
					<form class="relative my-4" on:submit={onSubmit}>
						<input
							type="email"
							aria-label="Email for newsletter"
							placeholder="tim@apple.com"
							autocomplete="email"
							required={true}
							class="mt-1 block w-full rounded-md border-gray-300 bg-white px-4 py-2 pr-32 text-gray-900 focus:border-blue-500 focus:ring-blue-500 dark:bg-gray-800 dark:text-gray-100"
						/><button
							class="absolute right-1 top-1 flex h-8 w-28 items-center justify-center rounded bg-gray-100 px-4 pt-1 font-medium text-gray-900 dark:bg-gray-700 dark:text-gray-100"
							type="submit">Subscribe</button
						>
					</form>
-->
        </div>

    </article>
</div>
