<script lang="ts">
  import { fly, fade } from 'svelte/transition';
  import { onDestroy } from 'svelte';

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
    },
  ];

  let currentIndex = $state(0);

  function next() { currentIndex = (currentIndex + 1) % projects.length; }
  function prev() { currentIndex = (currentIndex - 1 + projects.length) % projects.length; }
</script>

<section class="h-full w-full flex items-center justify-center p-4 relative overflow-hidden">
  
  <button 
    onclick={prev}
    aria-label="Previous project"
    class="absolute left-4 md:left-10 z-20 p-4 rounded-full bg-white/5 border border-white/10 hover:bg-white/20 transition-all text-white active:scale-90"
  >
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
  </button>

  <div class="relative w-full max-w-xl h-112 flex items-center justify-center">
    {#key currentIndex}
      <div 
        in:fly={{ x: 100, duration: 500, opacity: 0 }} 
        out:fly={{ x: -100, duration: 500, opacity: 0 }}
        class="absolute inset-0 bg-slate-900/40 border border-white/10 backdrop-blur-xl p-8 md:p-12 rounded-4xl shadow-2xl flex flex-col items-center text-center justify-center"
      >
        <span class="text-cyan-400 font-mono text-xs uppercase tracking-[0.2em] mb-4">
          Project {currentIndex + 1} / {projects.length}
        </span>
        
        <h2 class="text-4xl md:text-5xl font-bold text-white mb-4 italic tracking-tight uppercase">
          {projects[currentIndex].title}
        </h2>
        
        <p class="text-slate-400 text-lg leading-relaxed mb-8">
          {projects[currentIndex].desc}
        </p>
        
        <div class="flex flex-wrap justify-center gap-2 mb-10">
          {#each projects[currentIndex].tech.split(' • ') as tool}
            <span class="px-3 py-1 bg-white/5 border border-white/10 rounded-lg text-xs text-slate-300 font-mono">
              {tool}
            </span>
          {/each}
        </div>

        <div class="flex flex-col sm:flex-row items-center gap-6">
          <a href={projects[currentIndex].live} target="_blank" class="neo-button">
            <span class="neo-inner">View Live</span>
          </a>

          <a href={projects[currentIndex].source} class="text-slate-400 hover:text-white transition-colors font-medium text-sm border-b border-transparent hover:border-white">
            Source Code
          </a>
        </div>
      </div>
    {/key}
  </div>

  <button 
    onclick={next}
    aria-label="Next project"
    class="absolute right-4 md:right-10 z-20 p-4 rounded-full bg-white/5 border border-white/10 hover:bg-white/20 transition-all text-white active:scale-90"
  >
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
  </button>

</section>

<style>
  /* The Godot-inspired Neo Glow */
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
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    /* Using Cyan and Emerald for that Godot look */
    background: conic-gradient(
      from 0deg,
      #22d3ee, /* cyan-400 */
      #34d399, /* emerald-400 */
      #3b82f6, /* blue-500 */
      #22d3ee
    );
    animation: rotate 4s linear infinite;
  }

  .neo-inner {
    position: relative;
    z-index: 1;
    display: block;
    background: #020617; /* Matches slate-950 */
    color: white;
    padding: 12px 32px;
    border-radius: 9999px;
    font-weight: 800;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .neo-button:hover {
    transform: scale(1.1);
  }

  @keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
</style>