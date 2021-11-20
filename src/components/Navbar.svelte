<script>
    let links = [
        {
            id: 1,
            title: "Home",
            href: "/",
        },
        {
            id: 2,
            title: "My Github",
            href: "https://github.com/mecinkari/",
        },
    ];
</script>

<nav
    class="flex w-full shadow-sm px-6 sm:px-12 md:px-24 border-b bg-white items-center justify-between"
>
    <span class="p-4 text-lg font-bold text-blue-500">Mecinkari</span>
    <div class="flex flex-row gap-x-4">
        {#each links as link}
            <a key={link.id} href={link.href}>{link.title}</a>
        {/each}
    </div>
</nav>
