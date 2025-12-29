<script lang="ts">
  import { fly, fade } from 'svelte/transition';
  import { onMount } from 'svelte';

  const projects = [
    {
      title: "simple clock app",
      tech: "svelte • css • ts",
      desc: "A Simple Clock app with Alarm and stop watch functionalities built using Svelte.",
      live: "https://clock-app-five-kappa.vercel.app/",
      source: "https://github.com/abdalkreem15/Clock-app" 
    },
    {
      title: "simple todo app",
      tech: "svelte • css • ts",
      desc: "A simple to-do list application built using Svelte 4 with local storage support.",
      live: "https://todo-list-sepia-iota.vercel.app/",
      source: "https://github.com/abdalkreem15/todo-list"
    }
  ];

  let currentIndex = $state(0);
  let direction = $state(1); // 1 for right, -1 for left

  function next() { 
    direction = 1;
    currentIndex = (currentIndex + 1) % projects.length; 
  }
  function prev() { 
    direction = -1;
    currentIndex = (currentIndex - 1 + projects.length) % projects.length; 
  }

  let visible = $state(false);
  onMount(() => visible = true);
</script>

{#if visible}
<section in:fade={{ duration: 400 }} class="h-full w-full flex flex-col items-center justify-start p-4 relative overflow-y-auto pt-28 pb-12">
  
  <!-- svelte-ignore a11y_consider_explicit_label -->
  <button onclick={prev} class="fixed left-4 md:left-10 top-1/2 -translate-y-1/2 z-30 p-4 rounded-full bg-white/5 border border-white/10 hover:bg-white/20 transition-all text-white active:scale-90 shadow-xl backdrop-blur-md">
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
  </button>

  <div class="relative w-full max-w-xl h-137.5 md:h-125 flex items-center justify-center">
    {#key currentIndex}
      <div 
        in:fly={{ x: 150 * direction, duration: 500, opacity: 0 }} 
        out:fly={{ x: -150 * direction, duration: 500, opacity: 0 }}
        class="absolute top-0 left-0 w-full h-full bg-slate-900/60 border border-white/10 backdrop-blur-xl p-8 md:p-12 rounded-4xl shadow-2xl flex flex-col items-center text-center justify-center"
      >
        <span class="text-cyan-400 font-mono text-xs uppercase tracking-[0.2em] mb-4">
          Project {currentIndex + 1} / {projects.length}
        </span>
        
        <h2 class="text-3xl md:text-5xl font-bold text-white mb-4 italic tracking-tight uppercase">
          {projects[currentIndex].title}
        </h2>
        
        <p class="text-slate-400 text-base md:text-lg leading-relaxed mb-8">
          {projects[currentIndex].desc}
        </p>
        
        <div class="flex flex-wrap justify-center gap-2 mb-10">
          {#each projects[currentIndex].tech.split(' • ') as tool}
            <span class="px-3 py-1 bg-white/5 border border-white/10 rounded-lg text-[10px] md:text-xs text-slate-300 font-mono">
              {tool}
            </span>
          {/each}
        </div>

        <div class="flex flex-col sm:flex-row items-center gap-6">
          <a href={projects[currentIndex].live} target="_blank" class="neo-button">
            <span class="neo-inner">View Live</span>
          </a>

          {#if projects[currentIndex].source}
            <a href={projects[currentIndex].source} target="_blank" class="text-slate-400 hover:text-white transition-colors font-medium text-sm border-b border-transparent hover:border-white">
              Source Code
            </a>
          {/if}
        </div>
      </div>
    {/key}
  </div>

  <!-- svelte-ignore a11y_consider_explicit_label -->
  <button onclick={next} class="fixed right-4 md:right-10 top-1/2 -translate-y-1/2 z-30 p-4 rounded-full bg-white/5 border border-white/10 hover:bg-white/20 transition-all text-white active:scale-90 shadow-xl backdrop-blur-md">
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
  </button>

</section>
{/if}

<style>
  /* Same neo-button styles as before */
  .neo-button {
    position: relative;
    padding: 2px;
    border-radius: 9999px;
    display: inline-block;
    overflow: hidden;
    transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  .neo-button::before {
    content: '';
    position: absolute;
    top: -50%; left: -50%; width: 200%; height: 200%;
    background: conic-gradient(from 0deg, #22d3ee, #34d399, #3b82f6, #22d3ee);
    animation: rotate 4s linear infinite;
  }
  .neo-inner {
    position: relative;
    z-index: 1;
    display: block;
    background: #020617;
    color: white;
    padding: 12px 32px;
    border-radius: 9999px;
    font-weight: 800;
    text-transform: uppercase;
  }
  @keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
</style>