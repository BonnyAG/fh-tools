<script lang="ts">
    // Import moment library
    import moment from 'moment';

    // Import Components
    import {
        TextInput,
        Grid,
        Row,
        Column, Button
    } from "carbon-components-svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';
    import Close from "carbon-icons-svelte/lib/Close.svelte";

    // Citation variables
    let fatherName: string = $state();
    let motherName: string = $state();
    let familySearchId: string = $state();
    let dateAccessed: string = $state(moment().format("MM/DD/YYYY"));

    function clearValues() {
        fatherName = "";
        motherName = "";
        familySearchId = "";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row>
        <Column>
            <TextInput labelText="Father's Name" placeholder="John Doe" class="min-w-[140px]" bind:value={fatherName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="FamilySearch ID (Father)" placeholder="ABCD-123" class="min-w-[140px]" bind:value={familySearchId} />
        </Column>
        <Column>
            <TextInput labelText="Mother's (Maiden) Name" placeholder="Jane Deer" class="min-w-[140px]" bind:value={motherName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput bind:date={dateAccessed} label="Date Accessed" />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4 mb-2">
        <Column>
            <Result 
                citation={`${fatherName} and ${motherName} Household (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
            />
        </Column>
    </Row>
    <!-- CLEAN FORM BUTTON -->
    <Row>
        <Column sm={{span: 3, offset: 1}} md={{span: 3, offset: 5}} lg={{span: 4, offset: 12}}>
            <Button class="w-full" kind="tertiary" on:click={clearValues} iconDescription="Clear" icon={Close} >Clear Form</Button>
        </Column>
    </Row>
</Grid>