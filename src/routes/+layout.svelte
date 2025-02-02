<script lang="ts">
  // ** STYLES **
  import "../app.css";
  import "carbon-components-svelte/css/white.css"; // TO_REMOVE
  
  // ** SVELTEKIT SETUP **
  interface Props {
    children?: import('svelte').Snippet;
  }
  let { children }: Props = $props();

  // ** VERCEL SETUP **
  import { dev } from '$app/environment';
  import { inject } from '@vercel/analytics';
  import { injectSpeedInsights } from '@vercel/speed-insights/sveltekit';
  
  inject({ mode: dev ? 'development' : 'production' });
  injectSpeedInsights();
</script>

{@render children?.()}