<script lang="ts">
	import { onMount } from 'svelte';
	import { getEntries, baseURL } from '../../api.svelte';

	let contacts = [];

	onMount(async () => {
		const data = await getEntries('/api/kontaktes?populate=%2A');
		contacts = data;
	});
</script>

<section class="text-gray-600 body-font">
	<div class="container px-5 py-24 mx-auto">
		<div class="flex flex-col text-center w-full mb-20">
			<h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-gray-900">Kontakt</h1>
			<p class="lg:w-2/3 mx-auto leading-relaxed text-base">
				Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has
				been the industry's standard dummy text ever since the 1500s, when an unknown printer took a
				galley of type and scrambled it to make a type specimen book. It has survived not only five
				centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
				It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum
				passages, and more recently with desktop publishing software like Aldus PageMaker including
				versions of Lorem Ipsum.
			</p>
		</div>
		<div class="contacts-container">
			{#each contacts as contact}
				<div class="flex flex-wrap -m-2">
					<div class="p-8 w-full">
						<div class="h-full flex flex-col items-center border-gray-200 border p-4 rounded-lg">
							{#if contact.attributes.Bild.data}
								<div class="w-16 h-16 mb-2">
									<img
										alt={contact.attributes.Bild.data.attributes.alternativeText}
										class="object-cover flex-shrink-0"
										src="{baseURL}{contact.attributes.Bild.data.attributes.url}"
									/>
								</div>
							{/if}
							<h2 class="title-font font-medium">
								{contact.attributes.Name}
							</h2>
							<div>
								<p>{contact.attributes.Strasse}</p>
								<p>{contact.attributes.PLZ} {contact.attributes.Ort}</p>
								{#if contact.attributes.Email}
									<p>{contact.attributes.Email}</p>
								{/if}
								{#if contact.attributes.Telefonnummer}
									<p>Tel: {contact.attributes.Telefonnummer}</p>
								{/if}
								{#if contact.attributes.FAX}
									<p>Fax: {contact.attributes.FAX}</p>
								{/if}
								{#if contact.attributes.Sonstiges}
									{contact.attributes.Sonstiges}
								{/if}
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<style windi:preflights:global windi:safelist:global>
	.contacts-container {
		text-align: center;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
	}
</style>
