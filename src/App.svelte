<script>
  import FeedbackForm from './components/FeedbackForm.svelte'
  import FeedbackList from './components/FeedbackList.svelte'
  import FeedbackStats from './components/FeedbackStats.svelte'

  let feedbacks = [ 
    {id: 1, rating: 10, text: "heheh"},
    {id:2, rating: 9, text: "heheh2"},
    {id: 3, rating: 7, text: "heheh3"},
    {id: 4, rating: 8, text: "hehe4h"},
  ]
  
  $: average = feedbacks.reduce((a, {rating}) => a + rating , 0) / feedbacks.length

  $:count = feedbacks.length

  const addFeedback = (e) => {
    const newFeedback = e.detail
    feedbacks = [newFeedback, ...feedbacks]
  }

  const deleteFeedback = (e) => {
    const itemId = e.detail
    feedbacks = feedbacks.filter(feedback => feedback.id !== itemId)
  }
</script>

<main>
  <FeedbackForm on:add-feedback={addFeedback} />
  <FeedbackStats {count} {average} />
  <FeedbackList {feedbacks} on:delete-feedback={deleteFeedback} />
</main>