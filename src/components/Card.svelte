<script>
    export let name;
    export let image;
</script>

<div class="bg-white flex flex-col items-center w-full shadow">
    <img class="overflow-hidden" src={image} alt="" />
    <div class="p-2 text-center">
        <p class="text-xl">{name}</p>
    </div>
</div>
