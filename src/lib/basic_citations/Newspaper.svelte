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
    let articleType: string;
    let publication: string;
    let dateOfArticle: string;
    let articleTitle: string;
    let pageNumber: string;
    let columnNumber: string;
    let databaseName: string;
    let databaseURL: string;
    let dateAccessed: string = moment().format("MM/DD/YYYY");

    function clearValues() {
        ancestorName = "";
        articleType = "";
        publication = "";
        dateOfArticle = "";
        articleTitle = "";
        pageNumber = "";
        columnNumber = "";
        databaseName = "";
        databaseURL = "";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Ancestor's Name" placeholder="James Smith" class="min-w-[140px]" bind:value={ancestorName} />
        </Column>
        <Column>
            <TextInput labelText="Article Type" placeholder="obituary" class="min-w-[140px]" bind:value={articleType} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Article Title" placeholder="Death of a Pioneer" class="min-w-[200px]" bind:value={articleTitle} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput label="Article Date" bind:date={dateOfArticle} />
        </Column>
        <Column>
            <TextInput labelText="Publication" placeholder="Deseret News" class="min-w-[140px]" bind:value={publication} />
        </Column>
        <Column>
            <TextInput labelText="Page Number" placeholder="4" class="min-w-[90px]" bind:value={pageNumber} />
        </Column>
        <Column>
            <TextInput labelText="Column Number" placeholder="2" class="min-w-[90px]" bind:value={columnNumber} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Database Name" placeholder="Utah Digital Newspapers" class="min-w-[140px]" bind:value={databaseName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
        <Column>
            <TextInput labelText="Database URL Type" placeholder="https://digitalnewspapers.org" class="min-w-[250px]" bind:value={databaseURL} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4 mb-2">
        <Column>
            <Result citation={`${ancestorName} ${articleType}, ${publication}, ${moment(dateOfArticle).format('D MMMM YYYY')}, "${articleTitle}," p. ${pageNumber}, column ${columnNumber}, database with images, ${databaseName} (${databaseURL} : accessed ${moment(dateAccessed).format('D MMMM YYYY')}).`} />
        </Column>
    </Row>
    <!-- CLEAN FORM BUTTON -->
    <Row>
        <Column sm={{span: 3, offset: 1}} md={{span: 3, offset: 5}} lg={{span: 4, offset: 12}}>
            <Button class="w-full" kind="tertiary" on:click={clearValues} iconDescription="Clear" icon={Close}>Clear Form</Button>
        </Column>
    </Row>
</Grid>