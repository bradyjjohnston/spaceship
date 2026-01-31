<script lang="ts">
  import { uiState } from '@/lib/ui.svelte';

  interface Post {
    id: string;
    data: {
      title: string;
      description: string;
    };
  }

  interface Props {
    posts: Post[];
  }

  let { posts }: Props = $props();
  let SearchDialog = $state<any>(null);

  $effect(() => {
    if (uiState.isSearchOpen && !SearchDialog) {
      import('./SearchDialog.svelte').then((m) => (SearchDialog = m.default));
    }
  });
</script>

{#if uiState.isSearchOpen && SearchDialog}
  <SearchDialog {posts} />
{/if}
