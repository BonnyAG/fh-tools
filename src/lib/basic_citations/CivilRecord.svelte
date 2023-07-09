<script>
    // Import libraries
    import moment from 'moment';

    // Import Components
    import { 
        Dropdown,
        TextInput,
        Grid,
        Row,
        Column
    } from "carbon-components-svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';

    // Citation Variables
    /** @type {string} */
    let ancestorName = "John Doe";
    /** @type {string} */
    let eventType = "birth";
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
    let siteURL = "www.ancestry.com";
    /** @type {string} */
    let dateAccessed = moment().format("MM/DD/YYYY");

    // Utility Variables
    /** List of all event types
	 * @enum
	 * @type {{id: string, text: string}[]}
	*/
	const EVENT_TYPES = [
		{ id: "birth", text: "Birth"},
		{ id: "marriage", text: "Marriage"},
		{ id: "divorce", text: "Divorce"},
		{ id: "death", text: "Death"},
	]
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
            <DateInput label="Event Date" bind:date={eventDate} />
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
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row>
        <Column>
            <Result
                citation={`${ancestorName} ${eventType}, ${moment(eventDate).format('D MMMM YYYY')}, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, "${collectionName}", ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
            />
        </Column>
    </Row>
</Grid>