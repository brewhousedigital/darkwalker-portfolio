<script>
    import {onMount} from "svelte";

    let artClasses = "";

    let showOptions = false;

    let themeIcon = "<i class='bi bi-sun'></i>";

    onMount(() => {
        let theme = localStorage.getItem("theme");
        if(theme === "light") {
            // Switching to light theme
            themeIcon = "<i class='bi bi-moon-stars'></i>";
            document.body.classList.add("light-theme");
            localStorage.setItem("theme", "light");
        }

        // Site is ready to be loaded
        document.body.style.opacity = "1";
    })


    function cleanUpAcidEffect() {
        document.querySelectorAll(".acid-effect-delete-me").forEach(item => {
            item.remove();
        });

        document.querySelectorAll(".acid-base").forEach(item => {
            item.classList.remove("acid-base");
        })

        document.querySelectorAll("figure").forEach(item => {
            item.style.width = "";
            item.style.height = "";
            item.style.overflow = "";
        })
    }

    function handleSilence() {
        cleanUpAcidEffect();

        artClasses = "";

        showOptions = false;
    }

    function handleVivid() {
        cleanUpAcidEffect();

        artClasses = "vivid";

        showOptions = false;
    }

    function handleAcid() {
        cleanUpAcidEffect();

        document.querySelectorAll("figure").forEach(item => {
            // Get attributes
            let image = item.querySelector("img");
            let width = image.width;
            // Include 24px for the figcaption height
            let height = image.height - 24;

            // Create a new image
            let copy = image.cloneNode(true);
            copy.classList.add("acid-effect-delete-me");

            // Append the new image
            item.appendChild(copy);

            // Update the original image with an animation class
            image.classList.add("acid-base");

            // Update the parent to hide the tranform
            item.style.width = width;
            item.style.height = height;
            item.style.overflow = "hidden";
        })

        artClasses = "acid";

        showOptions = false;

        setTimeout(() => {
            document.querySelectorAll(".acid-effect-delete-me").forEach(item => {
                item.classList.add("acid-effect-delete-me-load")
            })
        }, 500)
    }

    function handleTheme() {
        if(themeIcon.includes("bi-sun")) {
            // Switching to light theme
            themeIcon = "<i class='bi bi-moon-stars'></i>";
            document.body.classList.add("light-theme");
            localStorage.setItem("theme", "light");
        } else {
            // Switching to dark theme
            themeIcon = "<i class='bi bi-sun'></i>";
            document.body.classList.remove("light-theme");
            localStorage.removeItem("theme");
        }

        showOptions = false;
    }
</script>


<style>
    :global(body) {
        background-color: #222;
        color: #efefef;
        padding-top: 80px;
        opacity: 0;
        transition: opacity 300ms;
    }

    :global(body.light-theme) {background-color: #efefef; color: #222;}

    :global(::-webkit-scrollbar) {
        width: 20px;
    }

    :global(::-webkit-scrollbar-track) {
        background-color: #000;
    }

    :global(.light-theme::-webkit-scrollbar-track) {background-color: #eee;}

    :global(::-webkit-scrollbar-thumb) {
        border-radius: 100px;
        border: 5px solid transparent;
        background-clip: content-box;
        background-color: #2C3E50;
    }

    h1 {
        font-family: 'Shadows Into Light', cursive;
        background-color: #222;
        width: 100%;
        position: fixed;
        top: 0;
        z-index: 100;
    }

    h1 a {
        color: #efefef
    }

    :global(.light-theme h1) {background-color: #efefef!important;}
    :global(.light-theme h1 a) {color: #222!important}
    :global(.light-theme figcaption) {
        background-color: #efefef!important;
        color: rgba(34, 34, 34, 0.5)!important;
    }
    :global(.light-theme .options-open) {color: #222!important;}

    .options-open {
        color: #fff;
        position: fixed;
        z-index: 105;
        top: 12px;
        right: 12px;
        font-size: 19px;
    }

    @media screen and (min-width: 992px) {
        .options-open {
            font-size: 26px;
        }
    }

    #options {
        color: #efefef;
        position: fixed;
        top: 8px;
        right: 8px;
        border-radius: 4px;
        background-color: #2C3E50;
        padding: 20px;
        min-width: 160px;
        z-index: 110;
    }

    #options .btn {color: #fff;}

    #options .options-btn {
        border: 1px solid rgba(255, 255, 255, 0.1);
        width: 100%;
        display: block;
        margin-bottom: 12px;
    }

    #options .options-btn:last-of-type {
        margin-bottom: 0;
    }

    #options h2 {
        font-size: 14px;
        opacity: 0.5;
        margin-bottom: 12px;
    }

    #options .options-close {
        position: absolute;
        top: 0;
        right: 0;
    }



    /* Vivid animation */
    :global(#portfolio.vivid img) {
        animation-name: vivid-animation;
        animation-direction: alternate-reverse;
        animation-duration: 4s;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
    }
    @keyframes vivid-animation {
        0% {
            filter: hue-rotate(0deg) saturate(80%);

        }

        100% {
            filter: hue-rotate(100deg) saturate(160%);
        }
    }


    /* Acid animation */
    :global(#portfolio.acid img.acid-base) {
        animation-name: acid-animation;
        animation-direction: alternate-reverse;
        animation-duration: 20s;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
        animation-delay: 1s;
    }
    @keyframes acid-animation {
        0% {
            -webkit-transform: scaleY(1);
            -moz-transform: scaleY(1);
            -ms-transform: scaleY(1);
            -o-transform: scaleY(1);
            transform: scaleY(1);
        }
        33% {
            -webkit-transform: scaleY(1.2) skewY(-2deg) scaleX(1.2) translateZ(0);
            -moz-transform: scaleY(1.2) skewY(-2deg) scaleX(1.2) translateZ(0);
            -ms-transform: scaleY(1.2) skewY(-2deg) scaleX(1.2) translateZ(0);
            -o-transform: scaleY(1.2) skewY(-2deg) scaleX(1.2) translateZ(0);
            transform: scaleY(1.2) skewY(-2deg) scaleX(1.2) translateZ(0);
        }
        66% {
            -webkit-transform: scaleY(1.2) skewY(2deg) translateZ(0);
            -moz-transform: scaleY(1.2) skewY(2deg) translateZ(0);
            -ms-transform: scaleY(1.2) skewY(2deg) translateZ(0);
            -o-transform: scaleY(1.2) skewY(2deg) translateZ(0);
            transform: scaleY(1.2) skewY(2deg) translateZ(0);
        }
        100% {
            -webkit-transform: scaleY(1.1) scaleX(1.1);
            -moz-transform: scaleY(1.1) scaleX(1.1);
            -ms-transform: scaleY(1.1) scaleX(1.1);
            -o-transform: scaleY(1.1) scaleX(1.1);
            transform: scaleY(1.1) scaleX(1.1);
        }
    }
    :global(.acid-effect-delete-me) {
        position: absolute;
        left: 0;
        right: 0;
        filter: invert(1) brightness(0.9) saturate(0.8);
        top: 0;
        mix-blend-mode: difference;
        transition: opacity 0.6s ease;
        display: block;
        animation: acid-animation 20s infinite alternate ease;
        animation-delay: 0s;
        opacity: 0;
    }
    :global(.acid-effect-delete-me-load) {
        opacity: 0.7;
    }
</style>


<h1 class="text-center font-cursive py-3 mb-3">
    <a href="/" class="text-decoration-none" sveltekit:prefetch>daemon kelli art</a>
</h1>

<button type="button" class="btn options-open" on:click={() => {showOptions = !showOptions}}>
    <i class="bi bi-text-right"></i>
</button>

<div id="portfolio" class={artClasses}>
    <slot></slot>
</div><!-- end container -->

<div id="options" class={showOptions ? '' : 'd-none'}>
    <button type="button" class="btn options-close" on:click={() => {showOptions = !showOptions}}>
        <i class="bi bi-x"></i>
    </button>

    <h2>Galleries</h2>
    <a href="/" class="btn options-btn" on:click={() => {showOptions = !showOptions}} sveltekit:prefetch>Home</a>
    <a href="/the-elements" class="btn options-btn" on:click={() => {showOptions = !showOptions}} sveltekit:prefetch>The Elements</a>

    <hr>

    <h2>Art Views</h2>

    <button type="button" class="btn options-btn" on:click={handleSilence}>Silence</button>
    <button type="button" class="btn options-btn" on:click={handleVivid}>Vivid</button>
    <button type="button" class="btn options-btn" on:click={handleAcid}>Acid</button>

    <hr>

    <button type="button" class="btn options-btn" on:click={handleTheme}>{@html themeIcon} Theme</button>
</div>