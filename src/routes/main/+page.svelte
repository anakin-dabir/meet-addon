<script>
  import { onMount } from 'svelte';
  import { meet } from '@googleworkspace/meet-addons/meet.addons';

  const CLOUD_PROJECT_NUMBER = '829040809073';

  onMount(async () => {
    try {
      const session = await meet.addon.createAddonSession({
        cloudProjectNumber: CLOUD_PROJECT_NUMBER,
      });

      await session.createMainStageClient();

      console.log('Main stage client initialized');
    } catch (error) {
      console.error('Failed to initialize main stage:', error);
    }
  });
</script>

<main class="p-6">
  <div class="text-lg font-semibold">
    This is the add-on Main Stage.<br />
    Everyone in the call can see this.
  </div>

  <div class="mt-4 text-blue-700">
    Hello, world!
  </div>
</main>
