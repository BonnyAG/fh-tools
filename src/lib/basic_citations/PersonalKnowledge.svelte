<script>
    import "carbon-components-svelte/css/all.css";
    import moment from 'moment';
    import { DatePicker, DatePickerInput } from "carbon-components-svelte";

    let interviewee = "John Doe";
    let interviewer = "James Robert"
    let date = new Date();
    let city = "Eden";
    let county = "Graham";
    let state = "Arizona";
    let copied = false;

    function copyToClipboard() {
        let citation = `Personal Interview of ${interviewee} by ${interviewer} on ${moment(date).format('D MMMM YYYY')}, in possession of ${interviewer}, [address for private use], ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<div id="results" class="mt-4 p-4 border border-gray-300 rounded-md shadow-sm">
    <div >
        <!-- Interview Section -->
        <div class="flex gap-3 mb-2">
            <!-- Interviewee -->
            <div class="w-[35%]">
                <label for="name" class="inline-block text-sm font-medium text-gray-700">Interviewee</label>
                <div class="mt-1">
                <input type="text" bind:value={interviewee} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="John Doe" aria-describedby="name-description">
                </div>
            </div>
            <!-- Interviewer -->
            <div class="w-[35%]">
                <label for="fID" class="block text-sm font-medium text-gray-700">Interviewer</label>
                <div class="mt-1">
                <input type="text" bind:value={interviewer} name="fID" id="fID" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="ABCD-123" aria-describedby="fID-description">
                </div>
            </div>
            <!-- Date of Interview -->
            <div class="">
                <p class="block text-sm font-medium text-gray-700">Interview Date</p>
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

        <!-- Place Section -->
        <div class="flex gap-3">
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
    <button 
      on:click={copyToClipboard}
      class="mt-4 w-full inline-flex text-left rounded-md hover:bg-gray-200 transition bg-gray-100 px-3 py-2 text-sm font-medium text-gray-800">
      {`Personal Interview of ${interviewee} by ${interviewer} on ${moment(date).format('D MMMM YYYY')}, in possession of ${interviewer}, [address for private use], ${city != "" ? city : ""}${city == "" ? county + " County" : ", " + county}, ${state}.`}
    </button>
    <p class="{!copied ? "hidden" : ""} text-sm text-green-600 mt-2 font-bold">Copied Citation!</p>
</div>

<style>
    #results {
        border: 1px solid #D1D5DB;
    }
</style>