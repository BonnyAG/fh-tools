<script>
    // Import Components
    import { 
        ClickableTile,
        Tooltip 
    } from "carbon-components-svelte";
    
    // Import Icons
    import Copy from "carbon-icons-svelte/lib/Copy.svelte";

    /** Defines when the tooltip is diplayed 
     * @type {boolean} */
    let copied = $state(false);
    

    
   /**
    * @typedef {Object} Props
    * @property {string} citation
    * @property {(text: string) => void} [copy] - Override the default copy behavior of using the navigator.clipboard.writeText API to copy text
    */

   /** @type {Props} */
   let { citation, copy = async (citation) => {
        try {
            await navigator.clipboard.writeText(citation);
        } catch (e) {
            console.log(e);
        }
    } } = $props();
</script>

<ClickableTile 
    on:click
    on:click="{() => {
        if (citation !== undefined) {
            copy(citation);
            copied=true;
        }
    }}"
>
    <div class="flex justify-between">
        <span>{citation}</span>
        <Tooltip bind:open={copied} icon={Copy} iconDescription="Copy to Clipboard" align="end">
            <p>Copied!</p>
        </Tooltip>
    </div>
</ClickableTile>