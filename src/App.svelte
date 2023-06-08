<!-- Logic -->
<script>
	import FeedbackList from "./components/FeedbackList.svelte";
  import FeedbackForm from "./components/FeedbackForm.svelte";
  import FeedbackStats from "./components/FeedbackStats.svelte";
  import { feedbacks as FeedbackStore } from "./store";


$: count = $FeedbackStore.length;
$: average = $FeedbackStore.reduce((acc, curr) => acc + curr.rating, 0) / count;
</script>

<!-- Output -->
<main class="container">
  <FeedbackForm />
	<FeedbackStats {count} {average} />
	<FeedbackList />
</main>


<!-- Styling -->
<style>

</style>