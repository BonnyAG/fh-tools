<script>
    import {
      Header,
      SideNav,
      SideNavItems,
      SideNavLink,
      SideNavDivider,
      SkipToContent,
      Content,
      Column,
    } from "carbon-components-svelte";

    // Import icons
    import DocumentAdd from "carbon-icons-svelte/lib/DocumentAdd.svelte";
    import Help from "carbon-icons-svelte/lib/Help.svelte";
    import WorkflowAutomation from "carbon-icons-svelte/lib/WorkflowAutomation.svelte";
    
    /** Tracks state for side navigation
     * @type {boolean}
     */
    let isSideNavOpen = false;
    
    /** Defines which page should be highlighted
     * @type {string}
     */
    export let selected; 
  </script>
  
  <Header class="py-3" bind:isSideNavOpen>
    <svelte:fragment slot="skip-to-content">
      <SkipToContent />
    </svelte:fragment>
    <img class="w-8 mr-3" src="/fhtools_logo.png" alt="F.H. Tools Logo"/>
    <h2 class="text-white font-md">F.H Tools</h2>
  </Header>
  
  <SideNav bind:isOpen={isSideNavOpen}>
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
      <SideNavDivider />
      {#if selected === "changelog"}
        <SideNavLink icon={Help} text="Updates & FAQ" href="/changelog" isSelected />
      {:else}
        <SideNavLink icon={Help} text="Updates & FAQ" href="/changelog" />
      {/if}
    </SideNavItems>
  </SideNav>
  
  <Content>
    <Column>
      <slot name="container"/>
    </Column>
  </Content>
  