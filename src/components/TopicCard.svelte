<script>
    import moment from "moment";

    export let title, lastActive, replies, views, slug, id;
</script>


<div class="p-6 border border-gray-400 rounded-lg">
    <a href={"https://forum.freecodecamp.org/t/" + slug + "/" + id} target="_blank"
       class="font-semibold visited:text-black">{title}</a>
    <div class="flex mt-2">
        <div class="text-xs font-medium">Replies: {replies} | Views: {views} | Last
            Active: {moment(lastActive).startOf('second').fromNow()}</div>
    </div>
</div>

