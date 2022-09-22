<script lang="ts">
	import { getEntries, baseURL } from '../../api.svelte';
	import { onMount } from 'svelte';
	import DownloadIcon from '../../components/icons/download-icon.svelte';
	import PdfIcon from '../../components/icons/pdf-icon.svelte';
	import ImageIcon from '../../components/icons/image-icon.svelte';

	let buttonData = [];

	onMount(async () => {
		const data = await getEntries('/api/download?populate[Download][populate]=%2A');
		buttonData = data.attributes.Download;
		console.log(buttonData[0]);
	});
</script>

<section>
	<div class="container px-5 py-24 mx-auto">
		<div class="flex flex-wrap w-full mb-20">
			<div class="lg:w-1/2 w-full mb-6 lg:mb-0">
				<h1 class="sm:text-3xl text-2xl font-medium title-font mb-2 text-gray-900">Downloads</h1>
				<div class="h-1 w-40 bg-indigo-500 rounded" />
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
		{#if buttonData}
			{#each buttonData as button}
				{#if button.Datei}
					<div class="container">
						<a href={baseURL + button.Datei.data.attributes.url} download target="_blank">
							<button type="submit" class="downloadBtn">
								{#if button.Icon}
									{#if button.Icon === 'Download'}
										<DownloadIcon />
									{/if}
									{#if button.Icon === 'PDF'}
										<PdfIcon />
									{/if}
									{#if button.Icon === 'Bild'}
										<ImageIcon />
									{/if}
								{:else}
									<DownloadIcon />
								{/if}
								<div class="px-2">
									{button.Titel}
								</div>
							</button>
						</a>
					</div>
				{/if}
			{/each}
		{/if}
	</div>
</section>

<style>
	.downloadBtn {
		display: flex;
		align-items: center;
		padding: 12px;
		background-color: darkgrey;
		border-radius: 3px;
	}
</style>
