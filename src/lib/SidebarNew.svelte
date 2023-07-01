<script>
    import {
      Header,
      SideNav,
      SideNavItems,
      SideNavLink,
      SideNavDivider,
      SkipToContent,
      Content,
      Grid,
      Row,
      Column,
    } from "carbon-components-svelte";

    // Import icons
    import DataEnrichmentAdd from "carbon-icons-svelte/lib/DataEnrichmentAdd.svelte";
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
  
  <Header company="F.H" platformName="Tools" bind:isSideNavOpen>
    <svelte:fragment slot="skip-to-content">
      <SkipToContent />
    </svelte:fragment>
    <h1 class="text-white">F.H Tools</h1>
  </Header>
  
  <SideNav bind:isOpen={isSideNavOpen}>
    <SideNavItems>
      <SideNavLink icon={DocumentAdd} text="Basic Citation Builder" href="/" isSelected />
      <SideNavLink icon={DataEnrichmentAdd} text="Advanced Citation Builder" href="/advanced" />
      <SideNavLink icon={WorkflowAutomation} text="Soundex Converter" href="/soundex" />
      <SideNavDivider />
      <SideNavLink icon={Help} text="Updates & FAQ" href="/changelog" />
    </SideNavItems>
  </SideNav>
  
  <Content>
    <Grid>
      <Row>
        <Column>
          <slot name="container"/>
        </Column>
      </Row>
    </Grid>
  </Content>
  