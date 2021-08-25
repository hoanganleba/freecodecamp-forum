<script>
  import { onMount } from "svelte";
  import TopicCard from "./components/TopicCard.svelte";
  import { topics, users } from "./store";

  onMount(async () => {
    fetch("https://forum-proxy.freecodecamp.rocks/latest")
      .then((response) => response.json())
      .then((data) => {
        topics.set(data.topic_list.topics);
        users.set(data.users);
      });
  });
</script>

<main class="container mx-auto md:px-0 px-4 grid gap-y-6">
  <h1
    class="mb-4 py-6 text-center text-xl font-medium bg-green-100 rounded-lg text-green-900"
  >
    FreeCodeCamp Forum
  </h1>
  {#if $topics}
    {#each $topics as topic}
      <TopicCard
        title={topic.title}
        slug={topic.slug}
        id={topic.id}
        replies={topic.reply_count}
        views={topic.views}
        lastActive={topic.last_posted_at}
        posters={topic.posters}
      />
    {/each}
  {:else}
    <p>loading...</p>
  {/if}
</main>

<style lang="postcss" global>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>
