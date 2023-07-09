<script>
    // Import libraries
    import moment from 'moment';

    // Import Components
    import { 
        Dropdown,
        TextInput,
        Grid,
        Row,
        Column,
        ClickableTile,
        Tooltip,
        Toggle
    } from "carbon-components-svelte";

    // Import Icons
    import Copy from "carbon-icons-svelte/lib/Copy.svelte";

    // Citation Variables
    /** @type {string} */
    let type = "interview";
    /** @type {string} */
    let interviewee = "John Doe";
    /** @type {string} */
    let interviewer = "James Robert"
    /** @type {string} */
    let dateOfInterview = moment().format('MM/DD/YYYY');
    /** @type {string} */
    let localCity = "Eden";
    /** @type {string} */
    let localCounty = "Graham";
    /** @type {string} */
    let state = "Arizona";
    /** @type {string} */
    let internationalCity = "Neydens";
    /** @type {string} */
    let internationalCounty = "Haute-Savoie";
    /** @type {string} */
    let region = "Auvergne-Rhônes Alpes"
    /** @type {string} */
    let country = "France"

    // Utility Variables
    /** Defines when the tooltip is diplayed 
     * @type {boolean} */
     let copied = false;
    /** @type {boolean} */
    let internationalMode = false;
    /** List of all event types
	 * @enum
	 * @type {{id: string, text: string}[]}
	*/
	const EVENT_TYPES = [
		{ id: "interview", text: "Interview"},
		{ id: "email", text: "Email"},
	]
    /** Regex pattern for dates
     * @type {RegExp}
    */
    const datePattern = /\d{1,2}\/\d{1,2}\/\d{2,4}/

    /** Copies the content of the citation to the clipboard */
    function copyToClipboard() {
        let address = internationalMode ? `${internationalCity != "" ? internationalCity : ""}${internationalCounty == "" ? internationalCounty + " County" : ", " + internationalCounty}, ${region}, ${country}` : `${localCity != "" ? localCity : ""}${localCounty == "" ? localCounty + " County" : ", " + localCounty}, ${state}`
        let citation = `Personal ${type == "interview" ? "Interview of" : "Email from"} ${interviewee} ${type == "interview" ? "by" : "to"} ${interviewer} on ${moment(dateOfInterview).format('D MMMM YYYY')}, in possession of ${interviewer}, [address for private use], ${address}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-5">
        <Column class="min-w-full sm:min-w-0">
            <Dropdown
                titleText="Event Type"
                placeholder="Select Event Type"
                items={EVENT_TYPES}
                bind:selectedId={type}
			/>
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Interviewee" class="min-w-[140px]" bind:value={interviewee} />    
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Interviewer" class="min-w-[140px]" bind:value={interviewer} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput 
                labelText="Interview Date"
                placeholder="mm/dd/yyyy"
                bind:value={dateOfInterview} 
                invalid={!datePattern.test(dateOfInterview)}
                invalidText={!datePattern.test(dateOfInterview) ? "Please enter a date" : ""}
            />
        </Column>
    </Row>
    <Row class="mb-3">
        <Column>
            <Toggle size="sm" hideLabel labelA="International Address" labelB="International Address" bind:toggled={internationalMode}/>
        </Column>
    </Row>
    <Row class="">
        {#if internationalMode}
            <Column>
                <TextInput labelText="City" class="min-w-[140px]" bind:value={internationalCity} />
            </Column>
            <Column>
                <TextInput labelText="County" class="min-w-[140px]" bind:value={internationalCounty} />
            </Column>
            <Column class="mt-2 sm:mt-0">
                <TextInput labelText="Region" class="min-w-[140px]" bind:value={region} />
            </Column>
            <Column class="mt-2 sm:mt-0">
                <TextInput labelText="Country" class="min-w-[140px]" bind:value={country} />
            </Column>
        {:else}
            <Column>
                <TextInput labelText="City" class="min-w-[140px]" bind:value={localCity} />
            </Column>
            <Column>
                <TextInput labelText="County" class="min-w-[140px]" bind:value={localCounty} />
            </Column>
            <Column class="mt-2 sm:mt-0">
                <TextInput labelText="State" class="min-w-[140px]" bind:value={state} />
            </Column>
        {/if}
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4">
        <Column>
            <ClickableTile on:click={copyToClipboard}>
                <div class="flex justify-between">
                    <span>{`Personal ${type == "interview" ? "Interview of" : "Email from"} ${interviewee} ${type == "interview" ? "by" : "to"} ${interviewer} on ${moment(dateOfInterview).format('D MMMM YYYY')}, in possession of ${interviewer}, [address for private use], ${internationalMode ? `${internationalCity != "" ? internationalCity : ""}${internationalCounty == "" ? internationalCounty + " County" : ", " + internationalCounty}, ${region}, ${country}` : `${localCity != "" ? localCity : ""}${localCounty == "" ? localCounty + " County" : ", " + localCounty}, ${state}`}.`}</span>
                    <Tooltip bind:open={copied} icon={Copy} align="end">
                        <p>Copied!</p>
                    </Tooltip>
                </div>
                
            </ClickableTile>
        </Column>
    </Row>
</Grid>