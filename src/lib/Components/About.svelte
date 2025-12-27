<script lang="ts">
    import { onMount, onDestroy } from 'svelte'; // Added onDestroy
    import { fly } from 'svelte/transition';

    let visible = $state(false);
    let name = "Abd-alkareem";
    let displayName = $state("");
    let index = 0;
    let interval: any; // Store the interval ID

    onMount(() => {
        visible = true;
        
        interval = setInterval(() => {
            if (index < name.length) {
                displayName += name[index];
                index++;
            } else {
                clearInterval(interval);
            }
        }, 150);
    });

    // Cleanup when user switches windows
    onDestroy(() => {
        if (interval) clearInterval(interval);
    });
</script>

{#if visible}
    <div in:fly={{ y: 20, duration: 800 }} class="h-full w-full flex flex-col items-center justify-center p-8">
        <div class="max-w-2xl bg-white/5 border border-white/10 backdrop-blur-md rounded-3xl p-8 shadow-2xl">
            
            <div class="mb-8 border-b border-white/10 pb-6">
                <h2 class="text-4xl font-bold text-white mb-2 font-mono">
                    <span class="text-slate-500 opacity-50">Name:</span> 
                    {displayName}<span class="animate-cursor border-r-2 border-blue-400 ml-1"></span>
                </h2>
                <p class="text-blue-400 flex items-center gap-2 text-sm font-medium">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                    Tanta, Egypt
                </p>
            </div>

            <div class="space-y-4 text-slate-300 leading-relaxed text-lg">
                <p>
                    I've always been curious about how things work behind the screen. 
                    Right now, I’m teaching myself to build for the web using 
                    <span class="text-blue-400 font-medium">SvelteKit</span> and 
                    <span class="text-indigo-400 font-medium">Tailwind CSS</span>.
                </p>
                <p>
                    I also love bringing small ideas to life as games in 
                    <span class="text-emerald-400 font-medium">Godot</span>. 
                    I'm still learning the ropes, but I'm enjoying the process of turning a blank page into something interactive.
                </p>
            </div>
        </div>
    </div>
{/if}

<style>
    @keyframes blink {
        0%, 100% { opacity: 1; }
        50% { opacity: 0; }
    }
    .animate-cursor {
        animation: blink 1s step-end infinite;
    }
</style>