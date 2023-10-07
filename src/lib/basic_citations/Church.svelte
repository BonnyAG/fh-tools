<script lang="ts">
    // Import libraries
    import moment from 'moment';

    // Import Components
    import {
        Dropdown,
        TextInput,
        Grid,
        Row,
        Column,
        Button, Toggle
    } from "carbon-components-svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';
    import Close from "carbon-icons-svelte/lib/Close.svelte";

    // Citation Variables
    let ancestorName: string;
    let citationType: string = "church";
    let eventType: string = "baptism";
    let eventDate: string = moment().format("MM/DD/YYYY");
    let city: string;
    let county: string;
    let state: string;
    let country: string;
    let collectionName: string;
    let details: string;
    let siteURL: string = "www.ancestry.com"
    let dateAccessed: string = moment().format("MM/DD/YYYY");

    // Utility Variables
    let internationalMode: boolean = false;
    const CITATION_TYPES: {id: string, text: string}[] = [
        { id: "church", text: "Church Record"},
        { id: "civil", text: "Civil Record"},
    ]
	const CHURCH_EVENT_TYPES: {id: string, text: string}[] = [
		{ id: "baptism", text: "Baptism"},
		{ id: "christening", text: "Christening"},
		{ id: "confirmation", text: "Confirmation"},
		{ id: "membership", text: "Membership"},
		{ id: "marriage", text: "Marriage"},
		{ id: "death and burial", text: "Death & Burial"},
	];
    const CIVIL_EVENT_TYPES: {id: string, text: string}[] = [
        { id: "birth", text: "Birth"},
        { id: "marriage", text: "Marriage"},
        { id: "divorce", text: "Divorce"},
        { id: "death", text: "Death"},
    ];

    function clearValues() {
        ancestorName = "";
        citationType = "church";
        eventType = "baptism";
        eventDate = moment().format("MM/DD/YYYY");
        city = "";
        county = "";
        state = "";
        country = "";
        collectionName = "";
        details = "";
        siteURL = "";
        dateAccessed = moment().format("MM/DD/YYYY");
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row class="mb-2">
        <Column>
            <TextInput labelText="Ancestor's Name" placeholder="John Doe" class="min-w-[140px]" bind:value={ancestorName} />
        </Column>

    </Row>
    <Row class="mb-2">
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Collection Name" placeholder="Arizona, births and christenings, 1909-1917" class="min-w-[140px]" bind:value={collectionName} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Collection Details" placeholder="Film #, Book #, Volume #, Page #..." class="min-w-[140px]" bind:value={details} />
        </Column>
    </Row>
    <Row class="mb-3">
        <Column>
            <Toggle size="sm" hideLabel labelA="International Address" labelB="International Address" bind:toggled={internationalMode}/>
        </Column>
    </Row>
    <Row class="mb-2">
        <Column>
            <TextInput labelText="City" class="min-w-[140px]" bind:value={city} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="County" class="min-w-[140px]" bind:value={county} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText={internationalMode ? "Region" : "State"} class="min-w-[140px]" bind:value={state} />
        </Column>
        {#if internationalMode}
            <Column class="mt-2 sm:mt-0">
                <TextInput labelText="Country" class="min-w-[140px]" bind:value={country} />
            </Column>
        {/if}
    </Row>
    <Row class="mb-2">
        <Column>
            <Dropdown
                    titleText="Citation Type"
                    placeholder="Select Citation Type"
                    class="min-w-[140px]"
                    items={CITATION_TYPES}
                    bind:selectedId={citationType}
            />
        </Column>
        <Column>
            <Dropdown
					titleText="Event Type"
					placeholder="Select Event Type"
                    class="min-w-[140px]"
					items={citationType === "church" ? CHURCH_EVENT_TYPES : CIVIL_EVENT_TYPES}
					bind:selectedId={eventType}
				/>
        </Column>
        <Column>
            <DateInput label="Event Date" bind:date={eventDate} />
        </Column>

    </Row>
    <Row class="mb-4">
        <Column>
            <TextInput labelText="Site Accessed" placeholder="www.ancestry.com" bind:value={siteURL} />
        </Column>
        <Column>
            <DateInput label="Date Accessed" bind:date={dateAccessed} />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mb-2">
        <Column>
            <Result
                citation={`${ancestorName} ${eventType}, ${moment(eventDate).format('D MMMM YYYY')}, ${city !== "" ? city : ""}${city === "" ? county + " County" : ", " + county}${state !== "" ? ", " + state : ""}${internationalMode ? ", " + country : ""}, "${collectionName}"${details ? `, ${details}` : ""}, ${siteURL}, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}
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