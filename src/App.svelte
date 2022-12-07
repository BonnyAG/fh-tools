<script>
  import CitationContainer from './lib/CitationContainer.svelte';

  let sidebarOpen = false;

  function comingSoon() {
    alert("Coming Soon");
  }

  function updateSidebar() {
    sidebarOpen = !sidebarOpen;
  }
</script>

<main>
  <div>
    <!-- Off-canvas menu for mobile, show/hide based on off-canvas menu state. -->
    <div class="relative z-40 transition-opacity md:hidden {sidebarOpen ? "ease-linear duration-300 opacity-100": "ease-linear duration-300 opacity-0 z-[-1]"}" role="dialog" aria-modal="true">
      <!--
        Off-canvas menu backdrop, show/hide based on off-canvas menu state.
  
        Entering: "transition-opacity ease-linear duration-300"
          From: "opacity-0"
          To: "opacity-100"
        Leaving: "transition-opacity ease-linear duration-300"
          From: "opacity-100"
          To: "opacity-0"
      -->
      <div class="fixed inset-0 bg-gray-600 bg-opacity-75 {sidebarOpen ? "" : "transition hidden"}"></div>
  
      <div class="fixed inset-0 z-40 flex transition {sidebarOpen ? " ease-in-out duration-300 transform translate-x-0" : "-translate-x-full ease-in-out duration-300 transform"}">
        <!--
          Off-canvas menu, show/hide based on off-canvas menu state.
  
          Entering: "transition ease-in-out duration-300 transform"
            From: "-translate-x-full"
            To: "translate-x-0"
          Leaving: "transition ease-in-out duration-300 transform"
            From: "translate-x-0"
            To: "-translate-x-full"
        -->
        <div class="relative flex w-full max-w-xs flex-1 flex-col bg-white transition {sidebarOpen ? "ease-in-out duration-300 opacity-100" : "ease-in-out duration-300 opacity-0"}">
          <!--
            Close button, show/hide based on off-canvas menu state.
  
            Entering: "ease-in-out duration-300"
              From: "opacity-0"
              To: "opacity-100"
            Leaving: "ease-in-out duration-300"
              From: "opacity-100"
              To: "opacity-0"
          -->
          <div class="absolute top-0 right-0 -mr-12 pt-2">
            <button on:click={updateSidebar} type="button" class="ml-1 flex h-10 w-10 items-center justify-center rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
              <span class="sr-only">Close sidebar</span>
              <!-- Heroicon name: outline/x-mark -->
              <svg class="h-6 w-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
  
          <div class="h-0 flex-1 overflow-y-auto pt-5 pb-4">
            <div class="flex flex-shrink-0 items-center px-4">
              <span class="p-4 bg-blue-100 rounded-md">🌳</span>
              <h1 class="font-bold text-2xl ml-2">F.H. Tools</h1>
            </div>
            <nav class="mt-5 space-y-1 px-2">
              <!-- Current: "bg-gray-100 text-gray-900", Default: "text-gray-600 hover:bg-gray-50 hover:text-gray-900" -->
              <a href="#" class="bg-gray-100 text-gray-900 group flex items-center px-2 py-2 text-base font-medium rounded-md">
                <!--
                  Heroicon name: outline/home
  
                  Current: "text-gray-500", Default: "text-gray-400 group-hover:text-gray-500"
                -->
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-gray-500 mr-4 flex-shrink-0 h-6 w-6">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
                </svg>
                Citation Builder
              </a>
  
              <button on:click={comingSoon} class="text-gray-600 hover:bg-gray-50 hover:text-gray-900 group flex items-center px-2 py-2 text-base w-full font-medium rounded-md">
                <!-- Heroicon name: outline/users -->
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-gray-400 group-hover:text-gray-500 mr-4 flex-shrink-0 h-6 w-6">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99" />
                </svg>
                Soundex Converter
              </button>
            </nav>
          </div>
        </div>
  
        <div class="w-14 flex-shrink-0">
          <!-- Force sidebar to shrink to fit close icon -->
        </div>
      </div>
    </div>
  
    <!-- Static sidebar for desktop -->
    <div class="hidden md:fixed md:inset-y-0 md:flex md:w-64 md:flex-col">
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div class="flex min-h-0 flex-1 flex-col border-r border-gray-200 bg-white">
        <div class="flex flex-1 flex-col overflow-y-auto pt-5 pb-4">
          <div class="flex flex-shrink-0 items-center px-4">
            <span class="p-4 bg-blue-100 rounded-md">🌳</span>
            <h1 class="font-bold text-2xl ml-2">F.H. Tools</h1>
          </div>
          <nav class="mt-5 flex-1 space-y-1 bg-white px-2">
            <!-- Current: "bg-gray-100 text-gray-900", Default: "text-gray-600 hover:bg-gray-50 hover:text-gray-900" -->
            <a href="#" class="bg-gray-100 text-gray-900 group flex items-center px-2 py-2 text-sm font-medium rounded-md">
              <!--
                Heroicon name: outline/home
  
                Current: "text-gray-500", Default: "text-gray-400 group-hover:text-gray-500"
              -->
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-gray-500 mr-3 flex-shrink-0 h-6 w-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
              </svg>
              Citation Builder
            </a>
  
            <button on:click={comingSoon} class="text-gray-600 hover:bg-gray-50 hover:text-gray-900 group flex items-center px-2 py-2 text-sm font-medium w-full rounded-md">
              <!-- Heroicon name: outline/users -->
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-gray-400 group-hover:text-gray-500 mr-3 flex-shrink-0 h-6 w-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99" />
              </svg>
              Soundex Converter
            </button>
          </nav>
        </div>
      </div>
    </div>
    <div class="flex flex-1 flex-col md:pl-64">
      <div class="sticky top-0 z-20 bg-white pl-1 pt-1 sm:pl-3 sm:pt-3 md:hidden">
        <button type="button" on:click={updateSidebar}  class="-ml-0.5 -mt-0.5 inline-flex h-12 w-12 items-center justify-center rounded-md text-gray-500 hover:text-gray-900 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-blue-500">
          <span class="sr-only">Open sidebar</span>
          <!-- Heroicon name: outline/bars-3 -->
          <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
          </svg>
        </button>
      </div>
      <div class="flex flex-col sm:h-screen">
        <main class="flex-1 py-6 z-10">
          <!-- Have components after this -->
          <CitationContainer />
        </main>
        <footer class="bg-gradient-to-t from-white via-white to-transparent z-30 sticky bottom-0 text-center w-[95%] sm:w-auto sm:mb-0 sm:text-right h-10 sm:mr-8">
          <p class="text-slate-400">&copy; {new Date().getFullYear()} Adam Bonny. All rights reserved. Built with <a class="text-blue-600 hover:text-blue-400 hover:underline" href="https://github.com/BonnyAG/fh-tools">Github</a> & <a class="text-blue-600 hover:text-blue-400 hover:underline" href="https://vercel.com">Vercel</a></p>
        </footer>
      </div>
    </div>
  </div>
</main>
