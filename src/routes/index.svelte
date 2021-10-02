<script>
    import PortfolioItem from "$lib/components/PortfolioItem.svelte";
    import portfolioItems from "$lib/portfolioItems.json";
</script>


{#each portfolioItems as item}
    <PortfolioItem file={item.filename} caption={item.caption} />
{/each}