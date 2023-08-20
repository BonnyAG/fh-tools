<script>
  import {
    Header,
    SideNav,
    SideNavItems,
    SideNavLink,
    SkipToContent,
    Content,
  } from "carbon-components-svelte";

    // Import icons
    import DocumentAdd from "carbon-icons-svelte/lib/DocumentAdd.svelte";
    import Help from "carbon-icons-svelte/lib/Help.svelte";
    import WorkflowAutomation from "carbon-icons-svelte/lib/WorkflowAutomation.svelte";

    // Import Logo
    import logo from '$lib/img/fhtools_logo.webp';
    
    /** Tracks state for side navigation
     * @type {boolean}
     */
    let isSideNavOpen = false;
    
    /** Defines which page should be highlighted
     * @type {string}
     */
    export let selected; 
  </script>
  
  <Header expandedByDefault class="py-3" company="" href="/" uiShellAriaLabel="Header Menu" bind:isSideNavOpen>
    <svelte:fragment slot="skip-to-content">
      <SkipToContent />
    </svelte:fragment>
    <a href="/" class="px-3 py-2 flex content-center">
      <img class="mr-3" width="42px" height="42px" src={logo} alt="F.H. Tools Logo"/>
      <h2 class="text-white font-md">F.H Tools</h2>
    </a>
  </Header>
  
  <SideNav ariaLabel="Sidebar Navigation Menu" class="z-10" bind:isOpen={isSideNavOpen}>
    <SideNavItems>
      {#if selected === "home"}
        <SideNavLink icon={DocumentAdd} text="Basic Citation Builder" href="/" isSelected />
      {:else}
        <SideNavLink icon={DocumentAdd} text="Basic Citation Builder" href="/" />
      {/if}
      {#if selected === "soundex"}
        <SideNavLink icon={WorkflowAutomation} text="Soundex Converter" href="/soundex" isSelected />
      {:else}
        <SideNavLink icon={WorkflowAutomation} text="Soundex Converter" href="/soundex" />
      {/if}
      {#if selected === "changelog"}
        <SideNavLink icon={Help} text="Updates & FAQ" href="/changelog" isSelected />
      {:else}
        <SideNavLink icon={Help} text="Updates & FAQ" href="/changelog" />
      {/if}
    </SideNavItems>
  </SideNav>

<Content class={isSideNavOpen ? "overflow-hidden" : ""}>
  <slot name="container"/>
</Content>