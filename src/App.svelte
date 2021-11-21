<script>
	import Navbar from "./components/Navbar.svelte";
	import Footer from "./components/Footer.svelte";
	import Card from "./components/Card.svelte";

	let meals = [];
	let categories = [];
	let currCategory = "Beef";

	function changeCategory(slug) {
		currCategory = slug;
		meals = [];
	}

	// Fetching meals data
	$: fetch(
		`https://www.themealdb.com/api/json/v1/1/filter.php?c=${currCategory}`
	)
		.then((r) => r.json())
		.then((data) => {
			meals = data["meals"];
		});

	// Fetching categories data
	$: fetch(`https://www.themealdb.com/api/json/v1/1/categories.php`)
		.then((d) => d.json())
		.then((data) => {
			categories = data["categories"];
		});

	// onMount(async function () {
	// 	const response = await fetch(endpoint);
	// 	const data = await response.json();
	// 	console.log(data["meals"]);
	// 	meals = data["meals"];
	// });
</script>

<div class="flex flex-col bg-gray-50 min-h-screen">
	<Navbar />
	<main class="container px-4 md:px-0 py-4">
		<p class="text-center mb-6 text-3xl">Meals</p>

		{#if categories}
			<p class="text-center mt-6 mb-3 text-xl">Select Category</p>
			<div class="flex w-full flex-wrap justify-center mb-6 gap-2">
				{#each categories as category, index}
					<span
						class={`p-2 ${
							category["strCategory"] == currCategory
								? "bg-red-500"
								: "bg-blue-500"
						} text-white cursor-pointer rounded`}
						on:click={changeCategory(category["strCategory"])}
					>
						{category["strCategory"]}
					</span>
				{/each}
			</div>
		{:else}
			<div>loading...</div>
		{/if}

		{#if meals}
			<div class="grid grid-cols-1 sm:grid-cols-3 md:grid-cols-5 gap-4">
				{#each meals as meal, index}
					<Card
						name={`${meal["strMeal"]}`}
						image={meal["strMealThumb"]}
						category={currCategory}
						id={meal["idMeal"]}
					/>
				{/each}
			</div>
		{:else}
			<div>Loading...</div>
		{/if}
	</main>
	<Footer />
</div>
