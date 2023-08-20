<svelte:head>
    <title>Basic Citation Builder - F.H Tools</title>
</svelte:head>

<script lang="js">
	// Import Carbon Components
	import { Dropdown } from "carbon-components-svelte";

	// Import Layout
	import Sidebar from '$lib/utilities/Sidebar.svelte';

	// Import Citations
	import CitationContainer from '$lib/utilities/CitationContainer.svelte';
    import Census from '$lib/basic_citations/Census.svelte';
    import Church from '$lib/basic_citations/Church.svelte';
    import FamilyTreeHousehold from '$lib/basic_citations/FamilyTreeHousehold.svelte';
    import FamilyTreePersonal from '$lib/basic_citations/FamilyTreePersonal.svelte'
    import PersonalKnowledge from '$lib/basic_citations/PersonalKnowledge.svelte';

	/** Tracks which citation template is being displayed
	 * @type {string} 
	*/
	let citationType = "tree-personal";

	/** List of all citation options
	 * @const
	 * @type {{id: string, text: string}[]}
	*/
	const CITATION_OPTIONS = [
		{ id: "tree-personal", text: "Family Tree Personal"},
		{ id: "tree-household", text: "Family Tree Household"},
		{ id: "census", text: "Census Record"},
		{ id: "church", text: "Church & Civil Record"},
		{ id: "knowledge-personal", text: "Personal Knowledge"},
	]
</script>

<Sidebar selected="home">
	<div slot="container" class="h-auto">
		<!-- HEADER -->
		<section class="mx-auto md:max-w-7xl">
			<h1 class="text-2xl font-semibold text-gray-900">Basic Citation Builder</h1>
		</section>
		<!-- MAIN CONTENT -->
		<section class="mx-auto md:max-w-7xl">
			<div class="py-1">
				<!-- SELECT CITATION TYPE -->
				<Dropdown
					titleText="Citation Type"
					placeholder="Select citation type"
					items={CITATION_OPTIONS}
					size="xl"
					bind:selectedId={citationType}
				/>
				
				<CitationContainer>
					<!-- DISPLAY CITATION -->
					{#if citationType === "tree-personal"}
						<FamilyTreePersonal />
					{:else if citationType === "tree-household"}
						<FamilyTreeHousehold />
					{:else if citationType === "census"}
						<Census />
					{:else if citationType === "church"}
						<Church />
					{:else if citationType === "knowledge-personal"}
						<PersonalKnowledge />
					{/if}
				</CitationContainer>
			</div>
		</section>
	</div>
</Sidebar>