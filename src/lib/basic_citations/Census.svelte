<script>
    // Import libraries
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

    // Citation Variables
    /** @type {string} */
    let fatherFirstName = "John";
    /** @type {string} */
    let motherFirstName = "Jane";
    /** @type {string} */
    let lastName = "Doe";
    /** @type {string} */
    let city = "Eden";
    /** @type {string} */
    let county = "Graham";
    /** @type {string} */
    let state = "Arizona";
    /** @type {number} */
    let censusYear = 1880;
    /** @type {string} */
    let enumerationDistrict = "2";
    /** @type {string} */
    let folio = "4";
    /** @type {string} */
    let pageNumber = "1";
    /** @type {string} */
    let siteURL = "www.ancestry.com";
    /** @type {string} */
    let dateAccessed = moment().format("MM/DD/YYYY");
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Father's First Name" class="min-w-[140px]" bind:value={fatherFirstName} />
        </Column>
        <Column>
            <TextInput labelText="Mother's First Name" class="min-w-[140px]" bind:value={motherFirstName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Last Name" class="min-w-[140px]" bind:value={lastName} />
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
            <TextInput labelText="State" class="min-w-[90px]" bind:value={state} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Census Year" class="min-w-[90px]"bind:value={censusYear} />
        </Column>
        <Column>
            <TextInput labelText="Enumeration District" class="min-w-[90px]" bind:value={enumerationDistrict} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Folio #" class="min-w-[90px]" bind:value={folio} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Page #" class="min-w-[90px]" bind:value={pageNumber} />
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
    <Row>
        <Column>
            <Result
                citation={`${fatherFirstName} ${motherFirstName != "" ? "and " + motherFirstName : ""} ${lastName} household, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, US Federal ${censusYear} Census, ${enumerationDistrict != "" ? "enumeration district " + enumerationDistrict + ", " : ""}${folio != "" ? "folio " + folio : ""}${pageNumber != "" ? ", page " + pageNumber : ""}, ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
            />
        </Column>
    </Row>
</Grid>