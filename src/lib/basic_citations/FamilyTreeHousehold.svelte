<script>
    import "carbon-components-svelte/css/all.css";
    import moment from 'moment';
    import { DatePicker, DatePickerInput } from "carbon-components-svelte";

    let fatherName = "John Doe";
    let motherName = "Jane Deer"
    let id = "ABCD-123";
    let date = new Date();
    let copied = false;

    function copyToClipboard() {
        let citation = `${fatherName} and ${motherName} Household (${id}), FamilyTree, www.familysearch.org, accessed ${moment(date).format('D MMMM YYYY')}.`
        copied = true;
        navigator.clipboard.writeText(citation);
    }
</script>

<div id="results" class="mt-4 p-4 border border-gray-300 rounded-md shadow-sm">
    <div class="flex flex-col md:flex-row md:items-end gap-3">
        <!-- Husband Name -->
        <div class="w-[100%] mb-1 md:mb-0 md:w-[35%]">
            <label for="name" class="inline-block text-sm font-medium text-gray-700">Father's Name</label>
            <div class="mt-1">
            <input type="text" bind:value={fatherName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="John Doe" aria-describedby="name-description">
            </div>
        </div>
        <!-- Wife Name -->
        <div class="w-[100%] mb-1 md:mb-0 md:w-[35%]">
            <label for="name" class="inline-block text-sm font-medium text-gray-700">Mother's Name</label>
            <div class="mt-1">
            <input type="text" bind:value={motherName} name="name" id="name" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="John Doe" aria-describedby="name-description">
            </div>
        </div>
        <!-- FamilySearch ID -->
        <div class="w-[100%] mb-3 md:mb-0 md:w-[35%]">
            <label for="fID" class="block text-sm font-medium text-gray-700">FamilySearch ID (Father)</label>
            <div class="mt-1">
            <input type="text" bind:value={id} name="fID" id="fID" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="ABCD-123" aria-describedby="fID-description">
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
    <button 
      on:click={copyToClipboard}
      class="mt-4 w-full inline-flex text-left rounded-md hover:bg-gray-200 transition bg-gray-100 px-3 py-2 text-sm font-medium text-gray-800">
      {`${fatherName} and ${motherName} Household (${id}), FamilyTree, www.familysearch.org, accessed ${moment(date).format('D MMMM YYYY')}.`}
    </button>
    <p class="{!copied ? "hidden" : ""} text-sm text-green-600 mt-2 font-bold">Copied Citation!</p>
</div>

<style>
    #results {
        border: 1px solid #D1D5DB;
    }
</style>