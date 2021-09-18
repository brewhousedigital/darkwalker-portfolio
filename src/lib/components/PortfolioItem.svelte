<script>
    export let file = "";
    export let caption = "";
    export let classes = "";
</script>


<figure class="mb-5 mx-auto position-relative">
    <img src="/images/art/{file}" {caption} class="img-fluid rounded d-block mx-auto {classes}">
    <figcaption>{caption}</figcaption>
</figure>


<style>
    figure {
        max-width: 768px;
    }

    figcaption {
        text-align: right;
        color: rgba(255, 255, 255, 0.5);
        background-color: #222;
        position: relative;
        z-index: 30;
        padding: 4px 12px 8px 8px;
    }
</style>