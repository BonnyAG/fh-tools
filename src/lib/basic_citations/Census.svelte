<script>
    // Import libraries
    import moment from 'moment';

    // Import Components
    import { 
        TextInput,
        Grid,
        Row,
        Column,
        ClickableTile,
        Tooltip 
    } from "carbon-components-svelte";

    // Import Icons
    import Copy from "carbon-icons-svelte/lib/Copy.svelte";

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

    // Utility Variables
    /** Defines when the tooltip is diplayed 
     * @type {boolean} */
    let copied = false;
    /** Regex pattern for dates
     * @type {RegExp}
    */
   const datePattern = /\d{1,2}\/\d{1,2}\/\d{2,4}/

    /** Copies the content of the citation to the clipboard */
    function copyToClipboard() {
        let citation = `${fatherFirstName} ${motherFirstName != "" ? "and " + motherFirstName : ""} ${lastName} household, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, US Federal ${censusYear} Census, ${enumerationDistrict != "" ? "enumeration district " + enumerationDistrict + ", " : ""}${folio != "" ? "folio " + folio : ""}${pageNumber != "" ? ", page " + pageNumber : ""}, ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Father's First Name" bind:value={fatherFirstName} />
        </Column>
        <Column>
            <TextInput labelText="Mother's First Name" bind:value={motherFirstName} />
        </Column>
        <Column>
            <TextInput labelText="Last Name" bind:value={lastName} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="City" bind:value={city} />
        </Column>
        <Column>
            <TextInput labelText="County" bind:value={county} />
        </Column>
        <Column>
            <TextInput labelText="State" bind:value={state} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Census Year" bind:value={censusYear} />
        </Column>
        <Column>
            <TextInput labelText="Enumeration District" bind:value={enumerationDistrict} />
        </Column>
        <Column>
            <TextInput labelText="Folio #" bind:value={folio} />
        </Column>
        <Column>
            <TextInput labelText="Page #" bind:value={pageNumber} />
        </Column>
    </Row>
    <Row class="mb-4">
        <Column>
            <TextInput labelText="Site Accessed" bind:value={siteURL} />
        </Column>
        <Column>
            <TextInput 
                labelText="Date Accessed"
                placeholder="mm/dd/yyyy"
                bind:value={dateAccessed} 
                invalid={!datePattern.test(dateAccessed)}
                invalidText={!datePattern.test(dateAccessed) ? "Please enter a date" : ""}
                />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row>
        <Column>
            <ClickableTile on:click={copyToClipboard}>
                <div class="flex justify-between">
                    <span>{`${fatherFirstName} ${motherFirstName != "" ? "and " + motherFirstName : ""} ${lastName} household, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, US Federal ${censusYear} Census, ${enumerationDistrict != "" ? "enumeration district " + enumerationDistrict + ", " : ""}${folio != "" ? "folio " + folio : ""}${pageNumber != "" ? ", page " + pageNumber : ""}, ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}</span>
                    <Tooltip bind:open={copied} icon={Copy} align="end">
                        <p>Copied!</p>
                    </Tooltip>
                </div>
                
            </ClickableTile>
        </Column>
    </Row>
</Grid>