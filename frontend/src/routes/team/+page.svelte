<script lang="ts">
	import { onMount } from 'svelte';
	import { getEntries, baseURL } from '../../api.svelte';

	let teamMembers = []; // explicit any -> let teamMembers: any[] = [];

	onMount(async () => {
		const data = await getEntries('/api/teammitglieds?populate=%2A');
		teamMembers = data;
	});
</script>

<section class="text-gray-600 body-font">
	<div class="container px-5 py-24 mx-auto">
		<div class="flex flex-col text-center w-full mb-20">
			<h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-gray-900">Unser Team</h1>
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
		<div class="flex flex-wrap">
			{#each teamMembers as member}
				<div class="p-2 lg:w-1/2 md:w-1/2 w-full">
					<div class="h-full flex border-gray-200 border p-4 rounded-lg">
						<img
							alt="team"
							class="w-22 h-22 bg-gray-100 object-cover object-center flex-shrink-0 rounded-full mr-4"
							src="{baseURL}{member.attributes.Bild.data.attributes.url}"
						/>
						<div class="flex-grow">
							<h2 class="text-gray-900 title-font font-medium">
								{member.attributes.Vorname}
								{member.attributes.Nachname}
							</h2>
							<p class="text-gray-500">{member.attributes.Position}</p>
							<p class="text-gray-900">{member.attributes.Beschreibung}</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<style windi:preflights:global windi:safelist:global>
</style>
