<script lang="ts">
    // Import moment library
    import moment from 'moment';

    // Import Components
    import {
        TextInput,
        Grid,
        Row,
        Column, Button,
    } from "carbon-components-svelte";
    import Result from '$lib/utilities/CitationResult.svelte';
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Close from "carbon-icons-svelte/lib/Close.svelte";

    // Citation Variables
    let ancestorName: string = $state();
    let familySearchId: string = $state();
    let dateAccessed: string = $state(moment().format("MM/DD/YYYY"));

    function clearValues() {
        ancestorName = "";
        familySearchId = "";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row>
        <Column>
            <TextInput labelText="Ancestor's Name" placeholder="John Smith" class="min-w-[140px]" bind:value={ancestorName} />
        </Column>
        <Column>
            <TextInput labelText="FamilySearch ID" placeholder="ABCD-123" class="min-w-[140px]" bind:value={familySearchId} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4 mb-2">
        <Column>
            <Result citation={`${ancestorName} (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`} />
        </Column>
    </Row>
    <!-- CLEAN FORM BUTTON -->
    <Row>
        <Column sm={{span: 3, offset: 1}} md={{span: 3, offset: 5}} lg={{span: 4, offset: 12}}>
            <Button class="w-full" kind="tertiary" on:click={clearValues} iconDescription="Clear" icon={Close}>Clear Form</Button>
        </Column>
    </Row>
</Grid>