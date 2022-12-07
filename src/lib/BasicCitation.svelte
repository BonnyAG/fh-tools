<script>
    let citationType = "Family Tree Personal";
    import Census from './basic_citations/Census.svelte';
    import Church from './basic_citations/Church.svelte';
    import CivilRecord from './basic_citations/CivilRecord.svelte';
    import FamilyTreeHousehold from './basic_citations/FamilyTreeHousehold.svelte';
    import FamilyTreePersonal from './basic_citations/FamilyTreePersonal.svelte'
    import PersonalKnowledge from './basic_citations/PersonalKnowledge.svelte';
</script>

<div>
    <label for="type" class="block text-sm font-medium text-gray-700">Citation Type</label>
    <select bind:value={citationType} id="type" name="type" class="mt-1 block w-full rounded-md border-gray-300 py-2 pl-3 pr-10 text-base focus:border-blue-500 focus:outline-none focus:ring-blue-500 sm:text-sm">
      <option selected>Family Tree Personal</option>
      <option>Family Tree Household</option>
      <option>Census</option>
      <option>Church Record</option>
      <option>Civil Record</option>
      <option>Personal Knowledge</option>
    </select>

    {#if citationType == "Family Tree Personal"}
        <FamilyTreePersonal />
    {:else if citationType == "Family Tree Household"}
        <FamilyTreeHousehold />
    {:else if citationType == "Census"}
        <Census />
    {:else if citationType == "Church Record"}
        <Church />
    {:else if citationType == "Civil Record"}
        <CivilRecord />
    {:else if citationType == "Personal Knowledge"}
        <PersonalKnowledge />
    {/if}
</div>

