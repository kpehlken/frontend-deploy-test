<script lang="ts">
	import { onMount } from 'svelte';
	import { getEntries } from '../api.svelte';

	let entries = [];

	onMount(async () => {
		const data = await getEntries('/api/therapiezentrum-unterseitens?populate=2%A');
		entries = data;
	});
</script>

<header class="text-gray-600 body-font">
	<div class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center">
		<a href="." class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0">
			<span class="ml-3 text-xl">Ankerland</span>
		</a>
		<nav class="md:ml-auto md:mr-auto flex flex-wrap items-center text-base justify-center">
			<a href="." class="nav-element">Start</a>
			<a href="news" class="nav-element">News</a>
			<a href="team" class="nav-element">Team</a>
			<a href="gallery" class="nav-element">Gallerie</a>
			<a href="contact" class="nav-element">Kontakt</a>
			<a href="downloads" class="nav-element">Download</a>
			{#each entries as entry}
				<a href={entry.attributes.Slug} class="nav-element">{entry.attributes.Titel}</a>
			{/each}
		</nav>
		<button
			class="inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0"
			>Button
			<svg
				fill="none"
				stroke="currentColor"
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="2"
				class="w-4 h-4 ml-1"
				viewBox="0 0 24 24"
			>
				<path d="M5 12h14M12 5l7 7-7 7" />
			</svg>
		</button>
	</div>
</header>

<slot />

<footer class="text-gray-600 body-font">
	<div
		class="container px-5 py-24 mx-auto flex md:items-center lg:items-start md:flex-row md:flex-nowrap flex-wrap flex-col"
	>
		<div class="w-64 flex-shrink-0 md:mx-0 mx-auto text-center md:text-left">
			<a
				href="."
				class="flex title-font font-medium items-center md:justify-start justify-center text-gray-900"
				><span class="ml-3 text-xl">Ankerland</span>
			</a>
		</div>
		<div class="flex-grow flex flex-wrap md:pl-20 -mb-10 md:mt-0 mt-10 md:text-left text-center">
			<div class="lg:w-1/4 md:w-1/2 w-full px-4">
				<h2 class="title-font font-medium text-gray-900 tracking-widest text-sm mb-3">Ankerland</h2>
				<nav class="list-none mb-10">
					<li>
						<a href="news" class="text-gray-600 hover:text-gray-800">News</a>
					</li>
					<li>
						<a href="team" class="text-gray-600 hover:text-gray-800">Team</a>
					</li>
					<li>
						<a href="gallery" class="text-gray-600 hover:text-gray-800">Gallery</a>
					</li>
					<li>
						<a href="contact" class="text-gray-600 hover:text-gray-800">Kontakt</a>
					</li>
					<li>
						<a href="downloads" class="text-gray-600 hover:text-gray-800">Download</a>
					</li>
				</nav>
			</div>
		</div>
	</div>
</footer>

<style windi:preflights:global windi:safelist:global lang="postcss">
	.nav-element {
		@apply mr-5 hover:text-gray-900;
	}
</style>
