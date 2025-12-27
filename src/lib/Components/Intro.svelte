<script lang="ts">
    import { onMount } from 'svelte';
    import { fly } from 'svelte/transition';

    let visible = $state(false);
    onMount(() => {
        visible = true;
    });
</script>
<section class="h-full w-full flex flex-col items-center justify-center p-8 text-center">
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-blue-500/10 blur-[120px] rounded-full -z-10"></div>

  {#if visible}
    <div in:fly={{ y: 20, duration: 800 }}>
      <h2 class="text-6xl md:text-8xl font-black tracking-tighter mb-4 bg-linear-to-b from-white to-slate-500 bg-clip-text text-transparent">
        WEB-DEVELOPER <br /> & GAME-DEVELOPER
      </h2>
      
      <p class="text-slate-400 text-lg md:text-xl max-w-2xl mx-auto leading-relaxed text-balance">
        I'm a <span class="text-white font-medium">developing programmer</span> currently exploring the world of web and game design. 
        I'm building my foundation with 
        <span class="text-blue-400 font-semibold drop-shadow-[0_0_8px_rgba(59,130,246,0.3)]">SvelteKit</span> and 
        <span class="text-indigo-400 font-semibold drop-shadow-[0_0_8px_rgba(129,140,248,0.3)]">Tailwind CSS</span>, 
        while experimenting with 
        <span class="text-cyan-400 font-semibold drop-shadow-[0_0_8px_rgba(34,211,238,0.5)]">small game projects</span> in 
        <span class="text-emerald-400 font-semibold drop-shadow-[0_0_8px_rgba(52,211,153,0.5)]">Godot</span>. 
        My goal is to learn by doing and share my progress through clean, interactive code.
    </p>

      <div class="mt-8 flex gap-4 justify-center">
        <button class="px-8 py-3 bg-white text-slate-950 font-bold rounded-full hover:scale-105 transition-transform">
          View Projects
        </button>
        <button class="px-8 py-3 border border-white/10 rounded-full hover:bg-white/5 transition-colors">
          Read Resume
        </button>
      </div>
    </div>
  {/if}
</section>