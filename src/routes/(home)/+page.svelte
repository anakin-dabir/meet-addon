<script>
  import { onMount } from 'svelte';
  import { meet } from '@googleworkspace/meet-addons/meet.addons';
  import { goto } from '$app/navigation';

  let sidePanelClient;
  let name = "Google Meet Add-on (Svelte)";

  const CLOUD_PROJECT_NUMBER = '463441100745';
  const MAIN_STAGE_URL = 'https://portfolio-hzfd.vercel.app/main'; // Update this

  async function startActivity() {
    try {
      await goto('/main');
    } catch (err) {
      console.error('Navigation failed:', err);
      error = 'Failed to navigate to main stage.';
    }
  }

  onMount(async () => {
    try {
      const session = await meet.addon.createAddonSession({
        cloudProjectNumber: CLOUD_PROJECT_NUMBER
      });
      sidePanelClient = await session.createSidePanelClient();
      console.log("Addon session and side panel client initialized");
    } catch (error) {
      console.error("Failed to initialize addon session:", error);
    }
  });
</script>

<main class="p-6">
  <h1 class="text-2xl font-bold text-blue-600">{name}</h1>
  <p class="mt-4 text-gray-600">
    This content is rendered inside the Meet Add-on iframe.
  </p>

  <button
    class="mt-6 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
    on:click={startActivity}
  >
    Launch Activity in Main Stage
  </button>
</main>
