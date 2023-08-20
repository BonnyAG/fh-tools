<svelte:head>
    <title>Soundex Converter - F.H Tools</title>
</svelte:head>

<script lang="ts">
	import Sidebar from '$lib/utilities/Sidebar.svelte';
    import {soundex} from 'soundex-code'
    import CitationContainer from "$lib/utilities/CitationContainer.svelte";
    import CitationResult from "$lib/utilities/CitationResult.svelte";
    import {Column, Grid, Row} from "carbon-components-svelte";
    import {TextInput} from 'carbon-components-svelte';

    let surname: string = "Smith";
    let code: string = soundex(surname);
</script>

<Sidebar selected="soundex">
    <div slot="container">
        <!-- HEADER -->
        <section class="mx-auto md:max-w-7xl">
            <h1 class="text-2xl font-semibold text-gray-900">Soundex Converter</h1>
        </section>
        <!-- MAIN CONTENT -->
        <section class="mx-auto md:max-w-7xl">
            <div class="py-1">
                <CitationContainer>
                    <Grid>
                        <Row class="mb-2">
                            <Column>
                                <TextInput labelText="Surname" placeholder="Doe" bind:value={surname} on:change={() => {code = soundex(surname)} } />
                            </Column>
                        </Row>
                        <Row>
                            <Column>
                                <CitationResult citation={code} />
                            </Column>
                        </Row>
                    </Grid>
                </CitationContainer>
            </div>
        </section>
    </div>
</Sidebar>
