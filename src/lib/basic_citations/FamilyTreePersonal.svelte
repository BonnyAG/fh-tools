<script>
    // Import moment library
    import moment from 'moment';

    // Import Components
    import { 
        TextInput,
        Grid,
        Row,
        Column,
    } from "carbon-components-svelte";
    import Result from '$lib/utilities/CitationResult.svelte';
    import DateInput from '$lib/utilities/DateInput.svelte';

    // Citation Variables
    /** @type {string} */
    let ancestorName = "John Doe";
    /** @type {string} */
    let familySearchId = "ABCD-123";
    /** @type {string} */
    let dateAccessed = moment().format("MM/DD/YYYY");
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row>
        <Column>
            <TextInput labelText="Ancestor's Name" class="min-w-[140px]" bind:value={ancestorName} />    
        </Column>
        <Column>
            <TextInput labelText="FamilySearch ID" class="min-w-[140px]" bind:value={familySearchId} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4">
        <Column>
            <Result citation={`${ancestorName} (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`} />
        </Column>
    </Row>
</Grid>