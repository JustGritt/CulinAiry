<svelte:head>
	<title>Home page</title>
</svelte:head>

<script>
    // Import global styles here
    import "../../global.css"
</script>

<main class="flex">
    <h1 class="bold">This is the <span class="accent">Quickstart</span> page</h1>
    <p>You can change routes by using links, <a href="/">return</a>.</p>

</main>

<style lang="scss">
    main {
        height: 100%;
        width: 100%;
        flex-direction: column;
        text-align: center;
        background: var(--secondary-color);

        p {
            margin-top: 0.5rem;
            font-size: var(--fs-large);
            a {
                color: var(--accent-color);
                font-size: inherit;
                text-decoration: none;
            }
        }
    }
</style>