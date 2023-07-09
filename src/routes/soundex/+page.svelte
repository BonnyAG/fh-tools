<svelte:head>
    <title>Soundex Converter - F.H Tools</title>
</svelte:head>

<script>
	import Sidebar from '$lib/utilities/Sidebar.svelte';
	import Soundex from '$lib/Soundex.svelte'
</script>

<Sidebar selected="soundex">
	<Soundex slot="container"/>
</Sidebar>
