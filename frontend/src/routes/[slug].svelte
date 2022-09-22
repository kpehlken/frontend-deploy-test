<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { getEntries, baseURL } from '../api.svelte';

	let entry;
	var lastPage;

	// Updates Content on Slug change
	$: if (lastPage != $page.params.slug) {
		update();
	}

	onMount(() => update());

	async function update() {
		lastPage = $page.params.slug;
		const data = await getEntries(
			`/api/therapiezentrum-unterseitens?populate=%2A&filters[slug]=${$page.params.slug}`
		);
		entry = data[0];
	}
</script>

<section class="text-gray-600 body-font">
	{#if entry}
		<div
			class="container mx-auto flex px-5 py-24 flex-col items-center {entry.attributes
				.Bildanordnung === 'Rechts'
				? ' md:flex-row-reverse'
				: 'md:flex-row'}"
		>
			{#if entry.attributes.Bild.data}
				<div class="lg:max-w-lg lg:w-full md:w-1/2 w-5/6 mb-10 md:mb-0">
					<img
						class="object-cover object-center rounded"
						alt={entry.attributes.Bild.data.attributes.alternativeText}
						src="{baseURL}{entry.attributes.Bild.data.attributes.url}"
					/>
				</div>
			{/if}
			<div
				class="lg:flex-grow md:w-1/2 {entry.attributes.Bildanordnung === 'Rechts'
					? 'lg:pr-24 md:pr-16'
					: 'lg:pl-24 md:pl-16'} flex flex-col md:items-start md:text-left items-center text-center"
			>
				<h1 class="title-font sm:text-4xl text-3xl mb-4 font-medium text-gray-900">
					{#if entry.attributes.Titel}
						{entry.attributes.Titel}
					{/if}
					<br class="hidden lg:inline-block" />
				</h1>
				<div class="mb-8 leading-relaxed">
					{#if entry.attributes.Text}
						{entry.attributes.Text}
					{/if}
				</div>
				<div class="flex justify-center">
					<button
						class="inline-flex text-white bg-blue-500 border-0 py-2 px-6 focus:outline-none hover:bg-blue-600 rounded text-lg"
						>Button</button
					>
					<button
						class="ml-4 inline-flex text-gray-700 bg-gray-100 border-0 py-2 px-6 focus:outline-none hover:bg-gray-200 rounded text-lg"
						>Button</button
					>
				</div>
			</div>
		</div>
	{/if}
</section>
