<script>
	import Navbar from "./components/Navbar.svelte";
	import Footer from "./components/Footer.svelte";
	import Card from "./components/Card.svelte";
	import { onMount } from "svelte";

	const endpoint =
		"https://www.themealdb.com/api/json/v1/1/filter.php?c=Seafood";

	$: meals = [];

	onMount(async function () {
		const response = await fetch(endpoint);
		const data = await response.json();
		console.log(data["meals"]);
		meals = data["meals"];
	});
</script>

<div class="flex flex-col bg-gray-50 min-h-screen">
	<Navbar />
	<main class="container px-4 md:px-0 py-4">
		<h1 class="text-center mb-6 text-3xl">Meals</h1>
		{#if !meals}
			<div>Loading...</div>
		{:else}
			<div class="grid grid-cols-1 sm:grid-cols-3 md:grid-cols-5 gap-4">
				{#each meals as meal}
					<Card name={meal["strMeal"]} image={meal["strMealThumb"]} />
				{/each}
			</div>
		{/if}
	</main>
	<Footer />
</div>
