<script lang="ts">
    import { onMount } from 'svelte';
    import { fly } from 'svelte/transition';

    let visible = $state(false);
    let name = "Abdalkareem";
    let displayName = $state("");
    let index = 0;

    onMount(() => {
        visible = true;
        
        // Typewriter logic
        const interval = setInterval(() => {
            if (index < name.length) {
                displayName += name[index];
                index++;
            } else {
                clearInterval(interval);
            }
        }, 150); // Speed of typing in milliseconds
    });
</script>

{#if visible}
    <div in:fly={{ y: 20, duration: 800 }} class="h-full w-full flex flex-col items-center justify-center p-8">
        <div class="max-w-2xl bg-white/5 border border-white/10 backdrop-blur-md rounded-3xl p-8 shadow-2xl">
            
            <div class="mb-8 border-b border-white/10 pb-6">
                <h2 class="text-4xl font-bold text-white mb-2 font-mono">
                    <span class="text-slate-500 opacity-50">Name:</span> 
                    {displayName}<span class="animate-pulse border-r-2 border-blue-400 ml-1"></span>
                </h2>
                <p class="text-blue-400 flex items-center gap-2 text-sm font-medium">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                    Tanta, Egypt
                </p>
            </div>

            </div>
    </div>
{/if}

<style>
    /* Pulse animation for the typing cursor */
    @keyframes pulse {
        0%, 100% { opacity: 1; }
        50% { opacity: 0; }
    }
    .animate-pulse {
        animation: pulse 1s cubic-bezier(0.4, 0, 0.6, 1) infinite;
    }
</style>