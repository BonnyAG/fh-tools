<script>
    import AdvancedCitation from './AdvancedCitation.svelte';
import BasicCitation from './BasicCitation.svelte'
    let advancedMode = false;

    function handleToggle() {
        advancedMode = advancedMode == true ? false : true;
    }
</script>

<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
    <h1 class="text-2xl font-semibold text-gray-900">Citation Builder</h1>
  </div>
  <div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
    <!-- Replace with your content -->
    <div class="py-4">
        <div class="inline-flex items-center rounded-md text-md font-medium">
            <p class="mr-3">Advanced Mode</p>
            <button type="button" on:click={handleToggle} class="{advancedMode ? "bg-indigo-600" : "bg-gray-200"} relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2" role="switch" aria-checked="false">
                <span class="sr-only">Use setting</span>
                <span class="{advancedMode ? "translate-x-5" : "translate-x-0"} pointer-events-none relative inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out">
                <span class="{advancedMode ? "opacity-0 ease-out duration-100" : "opacity-100 ease-in duration-200"} absolute inset-0 flex h-full w-full items-center justify-center transition-opacity" aria-hidden="true">
                    <svg class="h-3 w-3 text-gray-400" fill="none" viewBox="0 0 12 12">
                    <path d="M4 8l2-2m0 0l2-2M6 6L4 4m2 2l2 2" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    </svg>
                </span>
                <span class="{advancedMode ? "opacity-100 ease-in duration-200" : "opacity-0 ease-out duration-100"} absolute inset-0 flex h-full w-full items-center justify-center transition-opacity" aria-hidden="true">
                    <svg class="h-3 w-3 text-indigo-600" fill="currentColor" viewBox="0 0 12 12">
                    <path d="M3.707 5.293a1 1 0 00-1.414 1.414l1.414-1.414zM5 8l-.707.707a1 1 0 001.414 0L5 8zm4.707-3.293a1 1 0 00-1.414-1.414l1.414 1.414zm-7.414 2l2 2 1.414-1.414-2-2-1.414 1.414zm3.414 2l4-4-1.414-1.414-4 4 1.414 1.414z" />
                    </svg>
                </span>
                </span>
            </button>
        </div>
        <hr  class="mt-2 mb-3"/>
        
        {#if !advancedMode}
            <BasicCitation />
        {:else}    
            <AdvancedCitation/>
        {/if}
    </div>
    <!-- /End replace -->
  </div>