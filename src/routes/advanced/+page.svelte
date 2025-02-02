<script>
	import Sidebar from '$lib/utilities/Sidebar.svelte';
	import AdvancedCitation from '$lib/AdvancedCitation.svelte'
</script>

<Sidebar selected="advanced">
	{#snippet container()}
		<AdvancedCitation />
	{/snippet}
</Sidebar>