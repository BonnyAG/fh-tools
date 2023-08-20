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
        Toggle,
        Button
    } from "carbon-components-svelte";
    import Close from "carbon-icons-svelte/lib/Close.svelte";
    import DateInput from '$lib/utilities/DateInput.svelte';
    import Result from '$lib/utilities/CitationResult.svelte';

    // Citation Variables
    let type: string = "interview";
    let interviewee: string;
    let interviewer: string;
    let dateOfInterview: string = moment().format('MM/DD/YYYY');
    let city: string;
    let county: string;
    let region: string;
    let country: string;

    // Utility Variables
    let internationalMode: boolean = false;
	const EVENT_TYPES: {id: string, text: string}[] = [
		{ id: "interview", text: "Interview"},
		{ id: "email", text: "Email"},
	]

    function clearValues() {
        type = "interview";
        interviewee = "";
        interviewer = "";
        city = "";
        county = "";
        region = "";
        country = "";
        dateOfInterview = moment().format("MM/DD/YYYY");
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
            <TextInput labelText="Interviewee" placeholder="John Doe" class="min-w-[140px]" bind:value={interviewee} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="Interviewer" placeholder="Jane Doe" class="min-w-[140px]" bind:value={interviewer} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <DateInput bind:date={dateOfInterview} label="Interview Date" />
        </Column>
    </Row>
    <Row class="mb-3">
        <Column>
            <Toggle size="sm" hideLabel labelA="International Address" labelB="International Address" bind:toggled={internationalMode}/>
        </Column>
    </Row>
    <Row>
        <Column>
            <TextInput labelText="City" class="min-w-[140px]" bind:value={city} />
        </Column>
        <Column>
            <TextInput labelText="County" class="min-w-[140px]" bind:value={county} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText={internationalMode ? "Region" : "State"} class="min-w-[140px]" bind:value={region} />
        </Column>
        {#if internationalMode}
            <Column class="mt-2 sm:mt-0">
                <TextInput labelText="Country" class="min-w-[140px]" bind:value={country} />
            </Column>
        {/if}
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4 mb-2">
        <Column>
            <Result 
                citation={`Personal ${type === "interview" ? "Interview of" : "Email from"} ${interviewee} ${type === "interview" ? "by" : "to"} ${interviewer} on ${moment(dateOfInterview).format('D MMMM YYYY')}, in possession of ${interviewer}, [address for private use], ${city !== "" ? city : ""}${county !== "" ? ", " + county : ""}${region !== "" ? ", " + region : ""}, ${internationalMode ? country : "United States"}.`}
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