<script>
    // Import Carbon Components
    import { TextInput } from "carbon-components-svelte";

    // Utility Variables
    /** Regex pattern for dates
     * @type {RegExp}
    */
   const datePattern = /\d{1,2}\/\d{1,2}\/\d{2,4}/

   
   
   /**
    * @typedef {Object} Props
    * @property {string} date
    * @property {string} label
    */

   /** @type {Props} */
   let { date = $bindable(), label } = $props();
</script>

<TextInput 
    labelText={label}
    placeholder="mm/dd/yyyy"
    class="min-w-[140px]"
    bind:value={date}
    invalid={!datePattern.test(date)}
    invalidText={!datePattern.test(date) ? "Please enter a valid date" : ""}
/>