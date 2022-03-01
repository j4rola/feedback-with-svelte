<script>
    import { fade, scale } from 'svelte/transition'
    import FeedbackItem from './FeedbackItem.svelte' 
    export let feedback = [] 
    console.log(feedback)
</script>

{#each feedback as fb (fb.id)} 
    <div transition:fade>
        <FeedbackItem item={fb} on:delete-feedback/>   
    </div>      
{/each} 






