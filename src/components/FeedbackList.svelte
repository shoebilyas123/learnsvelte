<script>
    import {scale, fade} from 'svelte/transition';
    import { feedbacks as FeedbackStore } from "../store";

    import FeedbackItem from "./FeedbackItem.svelte";
</script>

{#each $FeedbackStore as fb (fb.id)}
<div in:scale out:fade>

    <FeedbackItem {fb}/>
</div>
{/each}