<script>
    // Import moment library
    import moment from 'moment';

    // Import Components
    import { 
        TextInput,
        Grid,
        Row,
        Column 
    } from "carbon-components-svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';

    // Citation variables
    /** @type {string} */
    let fatherName = "John Doe";
    /** @type {string} */
    let motherName = "Jane Deer";
    /** @type {string} */
    let familySearchId = "ABCD-123";
    /** @type {string} */
    let dateAccessed = moment().format("MM/DD/YYYY");
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row>
        <Column>
            <TextInput labelText="Father's Name" class="min-w-[140px]" bind:value={fatherName} />    
        </Column>
        <Column>
            <TextInput labelText="Mother's Name" class="min-w-[140px]" bind:value={motherName} />    
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="FamilySearch ID" class="min-w-[140px]" bind:value={familySearchId} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput bind:date={dateAccessed} label="Date Accessed" />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4">
        <Column>
            <Result 
                citation={`${fatherName} and ${motherName} Household (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
            />
        </Column>
    </Row>
</Grid>