<script>
    import {fade, scale} from 'svelte/transition'
    import FeedbackItem from "./FeedbackItem.svelte";
    export let feedbacks = []

</script>

{#each feedbacks as feedback (feedback.id) }
    <div in:scale out:fade>
        <FeedbackItem item={feedback} on:delete-feedback />
    </div>
{/each}

FeedbackList
