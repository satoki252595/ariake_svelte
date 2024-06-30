<script lang="ts">
  import { onMount } from "svelte";

  let eventListJson = [];
  let loading = true;

  onMount(async () => {
    const res = await fetch("http://localhost:3000/ariake_arena_events");
    eventListJson = await res.json();

    console.log(eventListJson);
    loading = false;
  });
</script>

<main>
  <div>
    {#if loading}
      <h1>ロード中ーーーー</h1>
    {:else}
      <h1>イベント一覧</h1>
      <hr />
      {#each eventListJson as eventList (eventList.id)}
        <div>
          イベント名:{eventList.name}
          開演時刻：{eventList.start_date}
          <hr />
        </div>
      {/each}
    {/if}
  </div>
</main>
