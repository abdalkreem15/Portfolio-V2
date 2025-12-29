<script lang="ts">
    import { onMount } from 'svelte';
    import { fly } from 'svelte/transition';

    // 1. Accept a function from the parent to change tabs
    let { onNavigate } = $props(); 

    let visible = $state(false);
    onMount(() => {
        visible = true;
    });

    // 2. Alert for the resume
    function handleResumeClick() {
        alert("The resume is not yet available. Please check back soon!");
    }
</script>

<section class="h-full w-full flex flex-col items-center justify-center p-8 text-center pt-28">
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-blue-500/10 blur-[120px] rounded-full -z-10"></div>

  {#if visible}
    <div in:fly={{ y: 20, duration: 800 }}>
      <h2 class="text-6xl md:text-8xl font-black tracking-tighter mb-4 bg-linear-to-b from-white to-slate-500 bg-clip-text text-transparent">
        WEB-DEVELOPER <br /> & GAME-DEVELOPER
      </h2>
      
      <div class="mt-8 flex gap-4 justify-center">
        <button 
          onclick={() => onNavigate('projects')}
          class="px-8 py-3 bg-white text-slate-950 font-bold rounded-full hover:scale-105 transition-transform cursor-pointer"
        >
          View Projects
        </button>
        
        <button 
          onclick={handleResumeClick}
          class="px-8 py-3 border border-white/10 rounded-full hover:bg-white/5 transition-colors text-white cursor-pointer"
        >
          Read Resume
        </button>
      </div>
    </div>
  {/if}
</section>