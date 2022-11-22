<script>
    import {createEventDispatcher} from 'svelte'
    import Card from "./Card.svelte";
  import FeedbackList from './FeedbackList.svelte';
    export let item

    const dispatch = createEventDispatcher()

    const handleDelete = (itemId) => {
        dispatch('delete-feedback', itemId )
    }

</script>

<Card>
    <div class="number-display">
        <span>{item.rating}</span>
    </div>
    <button class="close" on:click={ () => handleDelete(item.id)}>x</button>
    <p class="text-display">{item.text}</p>
</Card>

 <style>
    .number-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 40px;
    height: 40px;
    background: #ff6a95;
    color: #fff;
    border: 1px #eee solid;
    border-radius: 50%;
    padding: 10px;
    text-align: center;
    font-size: 19px;
  }
    .number-display span {
        margin-top: 20px;
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
    }

  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
    background: none;
    border: none;
    color: #000;
    font-size: 24px;
  }
 </style>