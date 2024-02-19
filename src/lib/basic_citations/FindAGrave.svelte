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
    let ancestorName: string;
    let birthYear: number | null = null;
    let deathYear: number | null = null;
    let memorialId: string;
    let dateAccessed: string = moment().format("MM/DD/YYYY");

    function clearValues() {
        ancestorName = "";
        birthYear = null;
        deathYear = null;
        memorialId = "";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Ancestor's Name" placeholder="John Smith" class="min-w-[140px]" bind:value={ancestorName} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Birth Year" placeholder="1816" class="min-w-[140px]" 
              bind:value={birthYear} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Death Year" placeholder="1876" class="min-w-[140px]" 
              bind:value={deathYear} />
        </Column>
    </Row>
    <Row>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Memorial #" placeholder="48537" class="min-w-[140px]" bind:value={memorialId} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4 mb-2">
        <Column>
            <Result citation={`Memorial page for ${ancestorName} (${birthYear === null ? "Unknown" : birthYear}-${deathYear === null ? "Unknown" : deathYear}), memorial #${memorialId}, FindaGrave, http://findagrave.com, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`} />
        </Column>
    </Row>
    <!-- CLEAN FORM BUTTON -->
    <Row>
        <Column sm={{span: 3, offset: 1}} md={{span: 3, offset: 5}} lg={{span: 4, offset: 12}}>
            <Button class="w-full" kind="tertiary" on:click={clearValues} iconDescription="Clear" icon={Close}>Clear Form</Button>
        </Column>
    </Row>
</Grid>