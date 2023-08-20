<script lang="ts">
    // Import libraries
    import moment from 'moment';

    // Import Components
    import {
        TextInput,
        Grid,
        Row,
        Column,
        Toggle,
        Button
    } from "carbon-components-svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';
    import Close from "carbon-icons-svelte/lib/Close.svelte";

    // Citation Variables
    let internationalCensus: boolean = false;
    let fatherFirstName: string;
    let motherFirstName: string;
    let lastName: string;
    let country: string;
    let city: string;
    let county: string;
    let state: string;
    let censusYear: number | null;
    let enumerationDistrict: string;
    let folio: string;
    let pageNumber: string;
    let siteURL: string = "www.ancestry.com";
    let dateAccessed: string = moment().format("MM/DD/YYYY");

    function clearValues() {
        internationalCensus = false;
        fatherFirstName = "";
        motherFirstName = "";
        lastName = "";
        country = "";
        city = "";
        county = "";
        state = "";
        censusYear = null;
        enumerationDistrict = "";
        folio = "";
        pageNumber = "";
        siteURL = "www.ancestry.com";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Father's First Name" placeholder="John" class="min-w-[140px]" bind:value={fatherFirstName} />
        </Column>
        <Column>
            <TextInput labelText="Mother's First Name" placeholder="Mary" class="min-w-[140px]" bind:value={motherFirstName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Last Name" placeholder="Smith" class="min-w-[140px]" bind:value={lastName} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <Toggle size="sm" labelA="International?" labelB="International?" labelText="International Mode" hideLabel bind:toggled={internationalCensus} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="City" class="min-w-[90px]" bind:value={city} />
        </Column>
        <Column>
            <TextInput labelText="County" class="min-w-[90px]" bind:value={county} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText={internationalCensus ? "Region" : "State"} class="min-w-[90px]" bind:value={state} />
        </Column>
        {#if internationalCensus}
            <Column>
                <TextInput labelText="Country" class="min-w-[90px]" bind:value={country} />
            </Column>
        {/if}
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Census Year" placeholder="1880" class="min-w-[90px]" bind:value={censusYear} />
        </Column>
        <Column>
            <TextInput labelText="Enumeration District" placeholder="2" class="min-w-[90px]" bind:value={enumerationDistrict} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Folio #" placeholder="4" class="min-w-[90px]" bind:value={folio} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Page #" placeholder="1" class="min-w-[90px]" bind:value={pageNumber} />
        </Column>
    </Row>
    <Row class="mb-4">
        <Column>
            <TextInput labelText="Site Accessed" bind:value={siteURL} />
        </Column>
        <Column>
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mb-2">
        <Column>
            <Result
                citation={`${fatherFirstName} ${motherFirstName !== "" ? "and " + motherFirstName : ""} ${lastName} household, ${city !== "" ? city : ""}${city === "" ? county + " County" : ", " + county}, ${state}, ${internationalCensus ? country : "US Federal"} ${censusYear ? censusYear : ""} Census, ${enumerationDistrict !== "" ? "enumeration district " + enumerationDistrict + ", " : ""}${folio !== "" ? "folio " + folio : ""}${pageNumber !== "" ? ", page " + pageNumber : ""}, ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
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