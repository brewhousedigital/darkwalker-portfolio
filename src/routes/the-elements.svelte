<script>
    import PortfolioItem from "$lib/components/PortfolioItem.svelte";
    import portfolioItems from "$lib/portfolioItems.json";

    let customGallery = [
        "carnelian.jpg",
        "moss-agate.jpg",
        "Iris.JPG",
        "fountain.JPG",
    ];

    let filteredGallery = portfolioItems.filter(item => customGallery.includes(item.filename));
</script>

<h2 class="text-center fw-light mb-5 mt-3" style="letter-spacing: 4px;">The Elements</h2>

{#each filteredGallery as item}
    <PortfolioItem file={item.filename} caption={item.caption} />
{/each}