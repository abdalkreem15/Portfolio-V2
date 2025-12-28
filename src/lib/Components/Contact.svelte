<script lang="ts">
  import { fade, fly } from 'svelte/transition';
  import { onMount } from 'svelte';

  let visible = $state(false);
  let copiedPhone = $state(false);

  // Form State
  let userName = $state("");
  let userMessage = $state("");

  const myEmail = "abdalkareemalkafoury@gmail.com";
  const phoneNumber = "+20 123 456 7890"; 

  function handleFormSubmit(e: Event) {
    e.preventDefault();
    
    // Encodes characters like spaces and newlines for the URL
    const subject = encodeURIComponent(`Portfolio Inquiry from ${userName}`);
    const body = encodeURIComponent(userMessage);
    
    // Triggers the user's default email app
    window.location.href = `mailto:${myEmail}?subject=${subject}&body=${body}`;
  }

  function copyPhone() {
    navigator.clipboard.writeText(phoneNumber);
    copiedPhone = true;
    setTimeout(() => (copiedPhone = false), 2000);
  }

  onMount(() => visible = true);
</script>

{#if visible}
<section in:fade={{ duration: 400 }} class="h-full w-full flex items-center justify-center p-4 overflow-y-auto">
  <div class="max-w-4xl w-full grid grid-cols-1 md:grid-cols-2 gap-8 bg-white/5 border border-white/10 backdrop-blur-xl rounded-4xl p-8 md:p-12 shadow-2xl">
    
    <div class="flex flex-col justify-between space-y-8">
      <div>
        <h2 class="text-4xl font-bold text-white mb-4">Let's talk</h2>
        <p class="text-slate-400 text-lg">
          Fill out the form, and it will prepare an email for you to send directly to me. No accounts or limits involved.
        </p>
      </div>

      <div class="space-y-4">
        <button 
          onclick={copyPhone}
          class="w-full flex items-center justify-between p-4 bg-white/5 rounded-2xl border border-white/10 hover:border-cyan-500/50 transition-all group"
        >
          <div class="flex flex-col items-start text-left">
            <span class="text-[10px] uppercase tracking-widest text-slate-500 font-mono">Mobile</span>
            <span class="text-white font-medium">{phoneNumber}</span>
          </div>
          <span class="text-xs text-cyan-400 font-bold uppercase">{copiedPhone ? 'Copied!' : 'Copy'}</span>
        </button>

        <div class="grid grid-cols-2 gap-4">
          <a href="https://github.com/abdalkareem15" target="_blank" class="p-4 bg-white/5 border border-white/10 rounded-2xl hover:bg-white/10 transition-all text-center">
            <span class="text-white font-bold font-mono text-sm uppercase">GitHub</span>
          </a>
          <a href="https://itch.io" target="_blank" class="p-4 bg-white/5 border border-white/10 rounded-2xl hover:bg-white/10 transition-all text-center">
            <span class="text-white font-bold font-mono text-sm uppercase">Itch.io</span>
          </a>
        </div>
      </div>
    </div>

    <form onsubmit={handleFormSubmit} class="flex flex-col gap-4">
      <div class="flex flex-col gap-1">
        <label for="name" class="text-xs font-mono text-slate-500 uppercase ml-2">Your Name</label>
        <input 
          type="text" 
          id="name" 
          bind:value={userName} 
          required 
          placeholder="Name..." 
          class="bg-white/5 border border-white/10 rounded-xl p-3 text-white focus:outline-none focus:border-cyan-500 transition-colors" 
        />
      </div>

      <div class="flex flex-col gap-1">
        <label for="msg" class="text-xs font-mono text-slate-500 uppercase ml-2">Message</label>
        <textarea 
          id="msg" 
          bind:value={userMessage} 
          required 
          placeholder="Write something..." 
          rows="4"
          class="bg-white/5 border border-white/10 rounded-xl p-3 text-white focus:outline-none focus:border-cyan-500 transition-colors resize-none"
        ></textarea>
      </div>

      <button type="submit" class="neo-button mt-2">
        <span class="neo-inner">Prepare Email</span>
      </button>
    </form>

  </div>
</section>
{/if}

<style>
  .neo-button {
    position: relative;
    padding: 2px;
    border-radius: 9999px;
    display: block;
    width: 100%;
    overflow: hidden;
    transition: transform 0.3s;
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
    padding: 14px;
    border-radius: 9999px;
    font-weight: 800;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .neo-button:hover { transform: scale(1.02); }

  @keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
</style>