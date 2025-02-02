<script lang="ts">
    interface Props {
        children?: import('svelte').Snippet;
    }

    let { children }: Props = $props();
</script>

<style>
    main {
        border-width: 1px !important;
        border-color: #8d8d8d !important;
    }
</style>

<main class="mt-4 p-4 shadow-md">
    {@render children?.()}
</main>