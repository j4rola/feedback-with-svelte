<script>
    import {v4 as uuidv4} from 'uuid'
    import Button from './Button.svelte'
    import Card from './Card.svelte' 
    import RatingSelect from './RatingSelect.svelte'  
    import {createEventDispatcher} from 'svelte'

    const dispatch = createEventDispatcher()

    let text = ''
    let rating = 10
    let btnDisabled = true
    let min = 10
    let message
    let newFeedback

    const handleSelect = (e) => {
        rating = e.detail
    }

    const handleInput = () => {
        if(text.trim().length <= min) {
            message = `Text must be at lest ${min} characters`
            btnDisabled = true
        } else {
            message = null
            btnDisabled = false 
        }

    }

    const handleSubmit = () => {
        
        if(text.trim().length > min ) {
            let newFeedback = {

                id: uuidv4(), 
                text,
                rating: +rating,
                 
            }

            console.log(newFeedback)  
            dispatch('handle-submit', newFeedback) 
            
            text = ''
        }
    }

</script>
 
<Card>
<header>How would you rate your service with us?</header>     
<form on:submit|preventDefault={() => handleSubmit(newFeedback)}>        
    <RatingSelect on:rating-select={handleSelect}/>     

    <div class="input-group">
        <input type="text" on:input={handleInput} bind:value = {text} placeholder="Tell us something that keeps you coming back">
        <Button disabled={btnDisabled} type="submit"  >Send</Button>  
    </div>
    {#if message}
        <div class='message'>
            {message}     
        </div>
    {/if}
</form>
</Card>


<style>
    header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message{
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>