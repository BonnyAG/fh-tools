<svelte:head>
    <title>Soundex Converter - F.H Tools</title>
</svelte:head>

<script>
	import Sidebar from '$lib/Sidebar.svelte';
	import Soundex from '$lib/Soundex.svelte'
    import FamilyTreeHousehold from '$lib/basic_citations/FamilyTreeHousehold.svelte';
    import FamilyTreePersonal from '$lib/basic_citations/FamilyTreePersonal.svelte';
</script>

<Sidebar selected="soundex">
	<Soundex slot="container"/>
</Sidebar>
