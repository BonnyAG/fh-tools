<script>
	import { ComboBox } from "carbon-components-svelte";
	
	// Filter Combobox function
	function shouldFilterItem(item, value) {
		if (!value) return true;
		return item.text.toLowerCase().includes(value.toLowerCase());
	}
	
	// Citation Types
	let citationTypeList = [
		{ id: "0", text: "Archives & Artifacts" },
		{ id: "1", text: "Business & Institutional" },
		{ id: "2", text: "Cemetery" },
		{ id: "3", text: "Census"}
	]
	
	// Citation Templates
	// 1. Archives & Artifacts
	let archivesTemplates = [
		{ id: "0", text: "Archived Artifact" },
		{ id: "1", text: "Archived Documents: Digitized" },
		{ id: "2", text: "Archived Manuscript Records" },
		{ id: "3", text: "Archived Manuscript Records"}
	]
	
	// Define variables
	let citationType, citationTemplate;
	
</script>

<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
	<h1 class="text-2xl font-semibold text-gray-900">Advanced Citation Builder</h1>
</div>
<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
	<div class="py-4">
		<ComboBox
			light
			titleText="Type"
	    	placeholder="Select citation type"
	  	  	items={citationTypeList}
			bind:selectedId={citationType}
	  		{shouldFilterItem}
		/>
		<div class="mt-4">
			<ComboBox
				light
				titleText="Template"
				placeholder="Select template"
				items={citationType == "0" ? archivesTemplates : []}
				bind:selectedId={citationTemplate}
				{shouldFilterItem}
			/>
		</div>	
	</div>
</div>