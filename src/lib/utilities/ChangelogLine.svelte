<script>
	import { Tag } from "carbon-components-svelte";

    
    
   /**
    * @typedef {Object} Props
    * @property {string} date
    * @property {{type:string, text:string}[]} lines
    */

   /** @type {Props} */
   let { date, lines } = $props();

   function getTagInfo(type) {
    switch (type) {
        case "improvement":
            return {color: "teal", text: "Improved"}
            break;
        case "bug":
            return {color: "red", text: "Bug Fix"}
            break;
        case "new":
            return {color: "green", text: "New"}
            break;
        default:
            return {color: "purple", text: "Change"}
            break;
    }
   }
</script>

<div>
    <h3 class="mt-3 text-lg font-bold">{date}</h3>
    <hr />
    <div class="my-2">
        {#each lines as line}
            <div class="flex items-center mb-1">
                <Tag class="shrink-0" type={getTagInfo(line.type).color}>{getTagInfo(line.type).text}</Tag>
                <p class="ml-1 text-sm">{line.text}</p>
            </div>
        {/each}
    </div>
</div>
