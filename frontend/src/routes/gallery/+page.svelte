<script context="module">
</script>

<script lang="ts">
	import { onMount } from 'svelte';
	import { getEntries, baseURL } from '../../api.svelte';

	let images = [];
	let currentImage;
	let count = 0;

	onMount(async () => {
		const data = await getEntries('/api/image-gallery?populate=%2A');
		images = data.attributes.Bilder.data;

		currentImage = images[count];
	});

	function handleClick(i) {
		if (i === -1 && count === 0) {
			count = images.length - 1;
		} else if (i !== -1 && count === images.length - 1) {
			count = 0;
		} else {
			count += i;
		}
		currentImage = images[count];
	}
</script>

<div class="flex items-center justify-center px-10">
	{#if currentImage}
		<button on:click={() => handleClick(-1)} class="button"> Vorheriges Bild </button>
		<div class="flex justify-center bg-gray-100 relative mb-4 mx-16 w-1/2">
			<img
				class="gallery-image p-8"
				src="{baseURL}{currentImage.attributes.url}"
				alt={currentImage.attributes.alternativeText}
			/>
		</div>
		<button on:click={() => handleClick(1)} class="button"> Nächstes Bild</button>
	{/if}
</div>

<style lang="postcss">
	.gallery-image {
		height: auto;
		width: 100%;
		aspect-ratio: 4/3;
	}

	.button {
		@apply inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0;
	}
</style>
