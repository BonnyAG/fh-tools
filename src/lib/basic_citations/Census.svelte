<script>
    import "carbon-components-svelte/css/all.css";
    import moment from 'moment';
    import { DatePicker, DatePickerInput } from "carbon-components-svelte";

    let fatherFirstName = "John";
    let motherFirstName = "Jane"
    let lastName = "Doe";
    let city = "Eden";
    let county = "Graham";
    let state = "Arizona";
    let censusYear = 1880;
    let ed = "2";
    let folio = "4";
    let page = "1";
    let site = "www.ancestry.com";
    let date = new Date();
    let copied = false;

    function copyToClipboard() {
        let citation = `${fatherFirstName} ${motherFirstName != "" ? "and " + motherFirstName : ""} ${lastName} household, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, US Federal ${censusYear} Census, ${ed != "" ? "enumeration district " + ed + ", " : ""}${folio != "" ? "folio " + folio : ""}${page != "" ? ", page " + page : ""}, ${site}, accessed ${moment(date).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<div id="results" class="mt-4 p-4 border border-gray-300 rounded-md shadow-sm">
    <div>
        <!-- Name Section -->
        <div class="flex flex-col md:flex-row gap-3 md:gap-0 mb-2">
            <div class="flex mb-3 gap-2 md:mb-0 md:w-[65%] md:mr-2">
                <!-- Father First Name -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Father's First Name</label>
                    <div class="mt-1">
                    <input type="text" bind:value={fatherFirstName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
                <!-- Mother First Name -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Mother's First Name</label>
                    <div class="mt-1">
                    <input type="text" bind:value={motherFirstName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
            </div>
            <!-- Last Name -->
            <div class="w-[100%] mb-3 md:w-[35%] md:mb-0">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">Last Name</label>
                <div class="mt-1">
                <input type="text" bind:value={lastName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                </div>
            </div>
        </div>

        <!-- Place Section -->
        <div class="flex gap-3 mb-3 md:mb-2">
            <!-- City -->
            <div class="w-[35%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">City</label>
                <div class="mt-1">
                <input type="text" bind:value={city} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                </div>
            </div>
            <!-- County -->
            <div class="w-[35%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">County</label>
                <div class="mt-1">
                <input type="text" bind:value={county} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                </div>
            </div>
            <!-- State -->
            <div class="w-[35%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">State</label>
                <div class="mt-1">
                <input type="text" bind:value={state} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                </div>
            </div>
        </div>

        <!-- Census Section -->
        <div class="flex flex-col md:flex-row gap-3 mb-2 w-[100%]">
            <div class="flex mb-3 gap-2 md:mb-0 md:w-[50%]">
                <!-- Census Year -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Census Year</label>
                    <div class="mt-1">
                    <input type="text" bind:value={censusYear} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
                <!-- Enumeration District -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Enumeration District</label>
                    <div class="mt-1">
                    <input type="text" bind:value={ed} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
            </div>
            <div class="flex mb-3 gap-2 md:mb-0 md:w-[50%]">
                <!-- Folio -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Folio #</label>
                    <div class="mt-1">
                    <input type="text" bind:value={folio} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
                <!-- Page -->
                <div class="w-[50%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">Page #</label>
                    <div class="mt-1">
                    <input type="text" bind:value={page} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Site Section -->
        <div class="flex flex-col md:flex-row gap-3 mb-2">
            <!-- Site -->
            <div class="w-[100%] mb-3 md:w-[35%] md:mb-0">
                <label for="fID" class="block text-sm font-medium text-gray-700">Site Accessed</label>
                <div class="mt-1">
                <input type="text" bind:value={site} name="fID" id="fID" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" placeholder="ABCD-123" aria-describedby="fID-description">
                </div>
            </div>
            <!-- Date Accessed -->
            <div>
                <p class="block text-sm font-medium text-gray-700">Date Accessed</p>
                <DatePicker datePickerType="single" bind:value={date} on:change light>
                    <DatePickerInput  
                        hideLabel
                        class="w-full text-sm font-medium text-gray-700 border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm"
                        labelText="Meeting date"
                        placeholder="mm/dd/yyyy"
                    />
                </DatePicker>
            </div>
        </div>
        
    </div>
    <button 
      on:click={copyToClipboard}
      class="mt-4 w-full inline-flex text-left rounded-md hover:bg-gray-200 transition bg-gray-100 px-3 py-2 text-sm font-medium text-gray-800">
      {`${fatherFirstName} ${motherFirstName != "" ? "and " + motherFirstName : ""} ${lastName} household, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, US Federal ${censusYear} Census, ${ed != "" ? "enumeration district " + ed + ", " : ""}${folio != "" ? "folio " + folio : ""}${page != "" ? ", page " + page : ""}, ${site}, accessed ${moment(date).format('D MMMM YYYY')}.`}
    </button>
    <p class="{!copied ? "hidden" : ""} text-sm text-green-600 mt-2 font-bold">Copied Citation!</p>
</div>

<style>
    #results {
        border: 1px solid #D1D5DB;
    }
</style>