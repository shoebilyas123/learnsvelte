<script>

    import FeedbackItem from "./FeedbackItem.svelte";
    export let feedbacks = [];
    console.log({feedbacks});
</script>

{#each feedbacks as fb (fb.id)}
    <FeedbackItem {fb} on:delete-fb/>
{/each}