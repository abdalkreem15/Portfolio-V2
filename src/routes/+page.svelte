<script lang="ts">
    import { fade } from "svelte/transition";
    import Intro from "$lib/Components/Intro.svelte";
	  import About from "$lib/Components/About.svelte";
    import Skills from "$lib/Components/Skills.svelte";

    let activeWindow = $state('intro');

    const tabs = [
        { id: 'intro', label: 'Intro' },
        { id: 'about', label: 'About' },
        { id: 'skills', label: 'Skills' },
        { id: 'projects', label: 'Projects' },
        { id: 'contact', label: 'Contact' },
    ];
</script>

<div class="h-svh w-full flex flex-col bg-slate-950 text-slate-200 overflow-hidden">
  
  <header class="w-full flex justify-center p-6 z-50">
    <nav class="flex items-center gap-1 bg-white/5 border border-white/10 backdrop-blur-xl p-1.5 rounded-2xl">
      {#each tabs as tab}
        <button 
          onclick={() => activeWindow = tab.id}
          class="px-6 py-2 rounded-xl text-sm font-medium transition-all duration-300
                 {activeWindow === tab.id 
                  ? 'bg-white/10 text-white shadow-lg' 
                  : 'hover:bg-white/5 text-slate-400 hover:text-slate-200'}"
        >
          {tab.label}
        </button>
      {/each}
    </nav>
  </header>

  <main class="grow relative">
    {#if activeWindow === 'intro'}
      <div in:fade={{ duration: 400 }} class="absolute inset-0">
        <Intro />
      </div>
    {:else if activeWindow === 'projects'}
      <div in:fade={{ duration: 400 }} class="absolute inset-0 flex items-center justify-center">
        <h2 class="text-4xl font-bold opacity-20 italic">Project Window coming soon...</h2>
      </div>
    {:else if activeWindow === 'skills'}
      <div in:fade={{ duration: 400 }} class="absolute inset-0 flex items-center justify-center">
        <Skills />
      </div>
    {:else if activeWindow === 'about'}
      <div in:fade={{ duration: 400 }} class="absolute inset-0 flex items-center justify-center">
        <About />
      </div>
    {:else if activeWindow === 'contact'}
      <div in:fade={{ duration: 400 }} class="absolute inset-0 flex items-center justify-center">
        <h2 class="text-4xl font-bold opacity-20 italic">Contact Window coming soon...</h2>
      </div>
    {/if}
    
    </main>
</div>