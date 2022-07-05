<script>
	import MobileMenu from './MobileMenu.svelte';
	import { REPO_URL } from '$lib/siteConfig';
	import NavLink from './NavLink.svelte';
	let isDark = false;
	if (typeof localStorage !== 'undefined') {
		if (
			localStorage.theme === 'dark' ||
			(!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
		) {
			isDark = true;
		}
	}
	function toggleDarkMode() {
		if (isDark) {
			document.documentElement.classList.remove('dark');
			localStorage.theme = 'light';
			isDark = false;
		} else {
			document.documentElement.classList.add('dark');
			localStorage.theme = 'dark';
			isDark = true;
		}
	}
</script>


<header class="navigation">
  <div class="navigation-inner">
    <nav class="brand-section">
      <MobileMenu />

      <a href="/" class="brand">
        <span>Kevin Unkrich</span>
      </a>
    </nav>
    <div>
      <nav>
		<NavLink href="/blog">Articles</NavLink>
		<!--
		<NavLink href="/projects">Projects</NavLink>
		-->
		<NavLink href="/about">About</NavLink>
      </nav>
    </div>
	<div class="toolbar-section">
		<nav class="social-nav">
		<!-- Github -->
		<a
			href={REPO_URL}
			aria-label="GitHub source"
			target="_blank"
		>
			<svg aria-hidden="true" class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
				<path
					fill-rule="evenodd"
					d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483
					0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608
					1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088
					2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988
					1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112
					6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202
					2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566
					4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019
					10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
					clip-rule="evenodd"
				/>
			</svg>
		</a>
		<a href="https://twitter.com/kevinunkrich" target="_blank" rel="noreferrer">
			<img style="background:none;" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAYAAACM/rhtAAAAAXNSR0IArs4c6QAAAgdJREFUWEftmC1PA0EQhq9NDYpABaUoEgghgEIRUASDJhDsOQwGheQ/IMDVQ9AYkPwAwocBS2kFECTJpSWZndnm5jLs7vUCcwk127vO7r7zdGZ27iqR8k9Fub7oX+Cw/5APwT5sUm+avd7aPnOG1WXn+2ymVGC9CcLimxfwprU69SsEZyarsO/zaw/gyQTLIjA6vQdy8dJYPpLoqBiUGNNE7umyB6azm1UYnQT1CSSP96+M0wuNfARZiHCCrbsPc2tvEYb+dRvG7u0IjGuHXwLBsgis7VyAB8nEaBhJgZwlxlE+dOBOZ3oZxsaBiXWqt9kYxA30CRTKihW6PpfyXcxqvg7FGs3eHjffzt/NiARr3U/zj52skCWrg2URGGH2xrvzKWJiDJEVZqM9eSRyZH/0mFrfm6B+geQX1UG8JqJOkjxLpWuMPfvz8UYqe1OBCBf8SFIrEM/ejOPcYzxhfIFZO7aOjb2zLU+C6gXmzWIXSoEcTUu8CaoVSK7wZoFlMZkFZ3Ng7GWzuOwCXSFGfaMr+ylrXbEXTPDvBPICTc+9rO3iAhPW3RRNbkCwNAKpQGNXwolIfWEoOd/YyxJUK5CXF+mo8+1K0I5nayg5uZtRK5CRpJizntPTnUDSSYzmBb4dcz7V6RM4IJR+7eas1IJBIDG+yk/vB9ULzMus0Hk+b1gL3TB0sW8ArqEwk582IgAAAABJRU5ErkJggg==" alt="Twitter">
		</a>
		<!-- <button
			aria-label="Toggle Dark Mode"
			class="ml-1 flex h-9 w-9 items-center justify-center rounded-lg bg-yellow-400 ring-yellow-400
			transition-all hover:ring-2 dark:bg-yellow-800"
			on:click={toggleDarkMode}
		>
			{#if isDark}
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					class="h-5 w-5 text-gray-800 dark:text-yellow-100"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728
						0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
					/>
				</svg>
			{:else}
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					class="w-5 h-5 text-gray-800 dark:text-gray-200"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
					/>
				</svg>
			{/if}
		</button> -->
	</div>
  </div>
</header>
