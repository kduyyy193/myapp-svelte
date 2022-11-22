<script>
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelec from "./RatingSelec.svelte";
  import {v4 as uuidv4} from 'uuid'
  import {createEventDispatcher} from 'svelte'

  const dispatch = createEventDispatcher()

  let text = ''
  let rating = 10
  let btnDisabled = true
  let min = 10
  let message

  const handleSelect = (e) => rating = e.detail
  const handleInput = () => {
    if(text.trim().length <= min ) {
        message = `Text must be at least ${min} characters`
        btnDisabled = true
    } else {
        message = ''
        btnDisabled = false
    }
  }

  const handleSubmit = () => {
    if(text.trim().length > min ) {
        const newFeedbacks = {
            id: uuidv4(),
            text,
            rating: +rating,
        }
        dispatch('add-feedback', newFeedbacks)

        text = ''
    }
  }

</script>
<Card>
    <header><h2>How would you rate your service with us</h2></header>
    <form on:submit|preventDefault={handleSubmit}>
        <RatingSelec on:rating-select={handleSelect}  />
        <div class="input-group">
            <input on:input={handleInput} bind:value={text} type="text" placeholder="Tell me us somting keeps you coming back">
        </div>
        <Button disabled={btnDisabled} type="submit">Send</Button>
        {#if message}
            <div class="message">
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
      margin-bottom: 15px;
    }
  
    input {
      flex-grow: 2;
      border: none;
      font-size: 16px;
      background-color: #fff;
      color: #000;
      padding: 4px;
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