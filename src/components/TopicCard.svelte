<script>
  import moment from "moment";
  import { users } from "../store";

  const getUsername = (user_id) => {
    const user = $users.filter((user) => user.id === user_id);
    console.log(user[0].avatar_template);
    return user[0].username;
  };

  const getUserAvatar = (user_id) => {
    const user = $users.filter((user) => user.id === user_id);
    if (user[0].avatar_template.match(/((http|https):)(www.)?/)) {
      return replaceRegAvatar(user[0].avatar_template);
    }
    return (
      "https://sea1.discourse-cdn.com/freecodecamp" +
      replaceRegAvatar(user[0].avatar_template)
    );
  };

  const replaceRegAvatar = (url) => {
    return url.replace(/{(.*?)}/, 40);
  };

  export let title, lastActive, replies, views, slug, id, posters;
</script>

<div
  class="p-6 border border-gray-400 rounded-lg flex justify-between items-center"
>
  <div>
    <a
      href={"https://forum.freecodecamp.org/t/" + slug + "/" + id}
      target="_blank"
      class="font-semibold visited:text-black">{title}</a
    >
    <div class="flex mt-2">
      <div class="text-xs font-medium">
        Replies: {replies} | Views: {views} | Last Active: {moment(lastActive)
          .startOf("second")
          .fromNow()}
      </div>
    </div>
  </div>
  <div class="flex -space-x-2 overflow-hidden">
    {#each posters as poster}
      <a
        class="font-semibold visited:text-black"
        href={"https://forum.freecodecamp.org/u/" + getUsername(poster.user_id)}
        target="_blank"
      >
        <img
          class="inline-block rounded-full ring-2 ring-white"
          src={getUserAvatar(poster.user_id)}
          alt={getUsername(poster.user_id)}
        />
      </a>
    {/each}
  </div>
</div>
