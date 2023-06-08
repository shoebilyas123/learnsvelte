<!-- Logic -->
<script>
	import FeedbackList from "./components/FeedbackList.svelte";

export let feedbacks = [
  {
    id: 1,
    rating: 10,
    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
  },
  {
    id: 2,
    rating: 9,
    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
  },
  {
    id: 3,
    rating: 8,
    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
  },
];

$: count = feedbacks.length;


const handleDelete = (eventParam)=>{
	let tempFBs = feedbacks.filter((fb)=>fb.id !== eventParam.detail);
	feedbacks = tempFBs;
}
</script>

<!-- Output -->
<main class="container">
	<h3>{count}</h3>
	<FeedbackList {feedbacks} on:delete-fb={handleDelete}/>
</main>


<!-- Styling -->
<style>

</style>