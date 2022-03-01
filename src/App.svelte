<script>

	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte'
	import FeedbackForm from './components/FeedbackForm.svelte' 


	let feedback = [{
		id: 1,
		rating: 10,
		text: 'lorem ipsum dolor sit amet consectetur'
	}, 
	{
		id: 2,
		rating: 8,
		text: 'adipisicing elit. consequuntur vel vitae'  
	}, 
	{
		id: 3,
		rating: 9,
		text: 'commodi alias voluptatem est voluptatem'
	}]

	$: count = feedback.length;
	$: average = feedback.reduce((a, {rating}) => a + rating, 0) / feedback.length 

	const deleteFeedback = (e) => {  
		const itemId = e.detail 
		feedback = feedback.filter((item) => item.id !== itemId)   
	}

	const addRating = (e) => {
		const newRating = e.detail
		
		feedback = [newRating, ...feedback] 
	}
	
</script>

<main class='container'>
	<FeedbackForm on:handle-submit={addRating}/>
	<FeedbackStats {count} {average}/>  
	<FeedbackList feedback = {feedback} on:delete-feedback={deleteFeedback}/>
</main>

<style>
	
</style>