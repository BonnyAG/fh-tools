<script>
    // Import moment library
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

    // Citation variables
    /** @type {string} */
    let fatherName = "John Doe";
    /** @type {string} */
    let motherName = "Jane Deer";
    /** @type {string} */
    let familySearchId = "ABCD-123";
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
        let citation = `${fatherName} and ${motherName} Household (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<Grid fullWidth noGutter>
    <!-- CITATION CONTENT -->
    <Row>
        <Column>
            <TextInput labelText="Father's Name" class="min-w-[140px]" bind:value={fatherName} />    
        </Column>
        <Column>
            <TextInput labelText="Mother's Name" class="min-w-[140px]" bind:value={motherName} />    
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput labelText="FamilySearch ID" class="min-w-[140px]" bind:value={familySearchId} />
        </Column>
        <Column class="mt-2 sm:mt-0">
            <TextInput 
                labelText="Date Accessed"
                placeholder="mm/dd/yyyy"
                class="min-w-[140px]"
                bind:value={dateAccessed} 
                invalid={!datePattern.test(dateAccessed)}
                invalidText={!datePattern.test(dateAccessed) ? "Please enter a date" : ""}
            />
        </Column>
    </Row>
    <!-- CITATION RESULT -->
    <Row class="mt-4">
        <Column>
            <ClickableTile on:click={copyToClipboard}>
                <div class="flex justify-between">
                    <span>{`${fatherName} and ${motherName} Household (${familySearchId}), FamilyTree, www.familysearch.org, accessed ${moment(dateAccessed).format('D MMMM YYYY')}.`}</span>
                    <Tooltip bind:open={copied} icon={Copy} align="end">
                        <p>Copied!</p>
                    </Tooltip>
                </div>
                
            </ClickableTile>
        </Column>
    </Row>
</Grid>