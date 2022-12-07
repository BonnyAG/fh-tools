<script>
    import "carbon-components-svelte/css/all.css";
    import moment from 'moment';
    import { DatePicker, DatePickerInput } from "carbon-components-svelte";

    let name = "John Doe";
    let type = "birth";
    let eventDate = new Date();
    let city = "Eden";
    let county = "Graham";
    let state = "Arizona";
    let collectionName = "Arizona, births and christenings, 1909-1917";
    let site = "www.ancestry.com"
    let date = new Date();
    let copied = false;

    function copyToClipboard() {
        let citation = `${name} ${type}, ${moment(eventDate).format('D MMMM YYYY')}, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, "${collectionName}", ${site}, accessed ${moment(date).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<div id="results" class="mt-4 p-4 border border-gray-300 rounded-md shadow-sm">
    <div>
        <!-- Name, Date, Place -->
        <div class="flex flex-col md:flex-row gap-3 mb-2">
            <!-- Name -->
            <div class="w-[100%] md:w-[35%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">Ancestor's Name</label>
                <div class="mt-1">
                <input type="text" bind:value={name} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="John Doe" aria-describedby="name-description">
                </div>
            </div>
            <div class="flex gap-2">
                <!-- City -->
                <div class="w-[35%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">City</label>
                    <div class="mt-1">
                    <input type="text" bind:value={city} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
                <!-- County -->
                <div class="w-[35%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">County</label>
                    <div class="mt-1">
                    <input type="text" bind:value={county} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
                <!-- State -->
                <div class="w-[35%]">
                    <label for="name" class="inline-block text-sm font-medium text-gray-700">State</label>
                    <div class="mt-1">
                    <input type="text" bind:value={state} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" aria-describedby="name-description">
                    </div>
                </div>
            </div>
        </div>

        <!-- Event Section -->
        <div class="flex flex-col md:flex-row gap-3 mb-2">
            <!-- Type of event -->
            <div class="w-[100%] md:w-[20%]">
                <label for="type" class="block text-sm font-medium text-gray-700">Citation Type</label>
                <select bind:value={type} id="type" name="type" class="mt-1 block w-full rounded-md border-gray-300 py-2 pl-3 pr-10 text-base focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm">
                <option value="birth" selected>Birth</option>
                <option value="marriage">Marriage</option>
                <option value="divorce">Divorce</option>
                <option value="confirmation">Death</option>
                </select>
            </div>
            <!-- Event Date -->
            <div class="">
                <p class="block text-sm font-medium text-gray-700">Event Date</p>
                <DatePicker datePickerType="single" bind:value={eventDate} on:change light>
                    <DatePickerInput  
                        hideLabel
                        class=" text-sm font-medium text-gray-700 border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
                        labelText="Meeting date"
                        placeholder="mm/dd/yyyy"
                    />
                </DatePicker>
            </div>
            <!-- Collection Name -->
            <div class="w-[100%] md:w-[60%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">Collection Name</label>
                <div class="mt-1">
                <input type="text" bind:value={collectionName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="John Doe" aria-describedby="name-description">
                </div>
            </div>
        </div>
        
        <!-- Site Section -->
        <div class="flex flex-col md:flex-row gap-3 mb-2">
            <!-- Site -->
            <div class="w-[100%] md:w-[35%]">
                <label for="fID" class="block text-sm font-medium text-gray-700">Site Accessed</label>
                <div class="mt-1">
                <input type="text" bind:value={site} name="fID" id="fID" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="ABCD-123" aria-describedby="fID-description">
                </div>
            </div>
            <!-- Date Accessed -->
            <div class="">
                <p class="block text-sm font-medium text-gray-700">Date Accessed</p>
                <DatePicker datePickerType="single" bind:value={date} on:change light>
                    <DatePickerInput  
                        hideLabel
                        class="w-full text-sm font-medium text-gray-700 border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
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
      {`${name} ${type}, ${moment(eventDate).format('D MMMM YYYY')}, ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}, "${collectionName}", ${site}, accessed ${moment(date).format('D MMMM YYYY')}.`}
    </button>
    <p class="{!copied ? "hidden" : ""} text-sm text-green-600 mt-2 font-bold">Copied Citation!</p>
</div>

<style>
    #results {
        border: 1px solid #D1D5DB;
    }
</style>