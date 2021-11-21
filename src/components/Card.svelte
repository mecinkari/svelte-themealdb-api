<script>
    export let id;

    let meals = [];

    $: fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${id}`)
        .then((r) => r.json())
        .then((data) => (meals = data["meals"][0]));
    console.log(meals);
</script>

{#if meals}
    <div class="bg-white flex flex-col p-4 w-full shadow">
        <img class="overflow-hidden" src={meals["strMealThumb"]} alt="" />
        <div class="mt-4 flex flex-col">
            <p class="text-lg">{meals["strMeal"] ? meals["strMeal"] : ""}</p>
            <p class="text-gray-500 text-sm mt-auto">
                {meals["strArea"] ? meals["strArea"] : ""} - {meals[
                    "strCategory"
                ]
                    ? meals["strCategory"]
                    : ""}
            </p>
        </div>
    </div>
{:else}
    <div>Loading...</div>
{/if}
