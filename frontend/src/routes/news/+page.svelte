<script lang="ts">
	import { onMount } from 'svelte';
	import { getEntries, baseURL } from '../../api.svelte';

	let blogEntries = [];

	onMount(async () => {
		const data = await getEntries('/api/blog?populate[blog_entries][populate]=%2A');
		blogEntries = data.attributes.blog_entries.data;
	});

	function date(date: string) {
		var d = new Date(date);
		return `Veröffentlich am: ${String(d.getDate()).padStart(2, '0')}.${String(
			d.getMonth() + 1
		).padStart(2, '0')}.${d.getFullYear()}`;
	}
</script>

<section class="text-gray-600 body-font">
	<div class="container px-5 py-24 mx-auto">
		<div class="flex flex-wrap w-full mb-20">
			<div class="lg:w-1/2 w-full mb-6 lg:mb-0">
				<h1 class="sm:text-3xl text-2xl font-medium title-font mb-2 text-gray-900">News</h1>
				<div class="h-1 w-20 bg-indigo-500 rounded" />
			</div>
			<p class="lg:w-1/2 w-full leading-relaxed text-gray-500">
				Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has
				been the industry's standard dummy text ever since the 1500s, when an unknown printer took a
				galley of type and scrambled it to make a type specimen book. It has survived not only five
				centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
				It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum
				passages, and more recently with desktop publishing software like Aldus PageMaker including
				versions of Lorem Ipsum.
			</p>
		</div>
		<div class="flex flex-wrap flex-col">
			{#if blogEntries}
				{#each blogEntries as entry}
					<div
						class="container mx-auto flex py-10 flex-row items-center w-screen {entry.attributes
							.Bildanordnung === 'Rechts'
							? ' md:flex-row-reverse'
							: ' md:flex-row'}"
					>
						{#if entry.attributes.Bild.data}
							<div class="lg:max-w-lg lg:w-full md:w-1/2 mb-10 md:mb-0">
								<img
									class="object-cover object-center rounded"
									alt={entry.attributes.Bild.data.attributes.alternativeText}
									src="{baseURL}{entry.attributes.Bild.data.attributes.url}"
								/>
							</div>
						{/if}
						<div
							class="lg:flex-grow {entry.attributes.Bild.data ? 'md:w-1/2' : 'md:w-full'} {entry
								.attributes.Bildanordnung === 'Rechts'
								? 'lg:pr-24 md:pr-16'
								: 'lg:pl-0 md:pl-0'} flex flex-col md:items-start md:text-left items-center text-center"
						>
							<h2 class="text-lg text-gray-900 font-medium title-font mb-6">
								{entry.attributes.Titel}
							</h2>
							<p class="text-gray-900 mb-6">
								{date(entry.attributes.publishedAt)}
							</p>
							<p class="leading-relaxed text-base">
								{entry.attributes.Beschreibung}
							</p>
						</div>
					</div>
				{/each}
			{/if}
		</div>
	</div>
</section>

<style windi:preflights:global windi:safelist:global>
</style>
