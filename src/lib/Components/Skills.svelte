<script lang="ts">
  import { onMount } from 'svelte';
  import { fly, fade } from 'svelte/transition';

  let visible = $state(false);
  onMount(() => visible = true);

  const skillGroups = [
    {
      title: "The Essentials",
      skills: [
        { name: "HTML", desc: "The skeleton of every project. I focus on semantic, accessible structures." },
        { name: "CSS & Tailwind", desc: "Styling with utility classes. I love building responsive, modern layouts." }
      ]
    },
    {
      title: "Logic & Frameworks",
      skills: [
        { name: "JavaScript", desc: "Learning the core logic behind interactivity and modern ES6+ features." },
        { name: "Svelte / SvelteKit", desc: "My primary tool for building fast web apps using runes and components." }
      ]
    },
    {
      title: "Game Development",
      skills: [
        { name: "Godot", desc: "Engineering small 2D/3D games. Exploring GDScript and game loops." }
      ]
    }
  ];
</script>

{#if visible}
<section in:fade={{ duration: 400 }} class="h-full w-full flex flex-col items-center justify-start p-6 pt-28 pb-12 overflow-y-auto">
  <div class="max-w-4xl w-full grid grid-cols-1 md:grid-cols-2 gap-6">
    {#each skillGroups as group, i}
      <div in:fly={{ y: 20, delay: i * 100 }} class="space-y-4">
        <h3 class="text-slate-500 font-mono text-sm uppercase tracking-widest pl-2">{group.title}</h3>
        {#each group.skills as skill}
          <div class="bg-white/5 border border-white/10 p-5 rounded-2xl backdrop-blur-sm hover:bg-white/10 transition-colors group">
            <h4 class="text-white font-bold text-lg mb-1 group-hover:text-cyan-400 transition-colors">{skill.name}</h4>
            <p class="text-slate-400 text-sm leading-relaxed">{skill.desc}</p>
          </div>
        {/each}
      </div>
    {/each}
  </div>
</section>
{/if}