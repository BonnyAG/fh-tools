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
        Tooltip 
    } from "carbon-components-svelte";

    // Import Icons
    import Copy from "carbon-icons-svelte/lib/Copy.svelte";

    // Citation Variables
    /** @type {string} */
    let ancestorName = "John Doe";
    /** @type {string} */
    let eventType = "baptism";
    /** @type {string} */
    let eventDate = moment().format("MM/DD/YYYY");
    /** @type {string} */
    let city = "Eden";
    /** @type {string} */
    let county = "Graham";
    /** @type {string} */
    let state = "Arizona";
    /** @type {string} */
    let collectionName = "Arizona, births and christenings, 1909-1917";
    /** @type {string} */
    let siteURL = "www.ancestry.com"
    /** @type {string} */
    let dateAccessed = moment().format("MM/DD/YYYY");

    // Utility Variables
    /** Defines when the tooltip is diplayed 
     * @type {boolean} */
    let copied = false;
    /** List of all event types
	 * @enum
	 * @type {{id: string, text: string}[]}
	*/
	const EVENT_TYPES = [
		{ id: "baptism", text: "Baptism"},
		{ id: "christening", text: "Christening"},
		{ id: "confirmation", text: "Confirmation"},
		{ id: "membership", text: "Membership"},
		{ id: "marriage", text: "Marriage"},
		{ id: "death and burial", text: "Death & Burial"},
	]
    /** Regex pattern for dates
     * @type {RegExp}
    */
   const datePattern = /\d{1,2}\/\d{1,2}\/\d{2,4}/

    /** Copies the content of the citation to the clipboard */
    function copyToClipboard() {
        let citation = `${ancestorName} ${eventType}, ${moment(eventDate).format('D MMMM YYYY')}, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, "${collectionName}", ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Ancestor's Name" class="min-w-[140px]" bind:value={ancestorName} />
        </Column>
        <Column>
            <TextInput labelText="City" class="min-w-[140px]" bind:value={city} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="County" class="min-w-[140px]" bind:value={county} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="State" class="min-w-[140px]" bind:value={state} />
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <Dropdown
					titleText="Event Type"
					placeholder="Select Event Type"
                    class="min-w-[140px]"
					items={EVENT_TYPES}
					bind:selectedId={eventType}
				/>
        </Column>
        <Column>
            <TextInput 
                labelText="Event Date"
                placeholder="mm/dd/yyyy"
                class="min-w-[140px]"
                bind:value={eventDate} 
                invalid={!datePattern.test(eventDate)}
                invalidText={!datePattern.test(eventDate) ? "Please enter a date" : ""}
                />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Collection Name" class="min-w-[140px]" bind:value={collectionName} />
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
                    <span>{`${ancestorName} ${eventType}, ${moment(eventDate).format('D MMMM YYYY')}, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, "${collectionName}", ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}</span>
                    <Tooltip bind:open={copied} icon={Copy} align="end">
                        <p>Copied!</p>
                    </Tooltip>
                </div>
                
            </ClickableTile>
        </Column>
    </Row>
</Grid>