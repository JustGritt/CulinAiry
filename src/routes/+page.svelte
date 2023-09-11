<svelte:head>
	<title>Home page</title>
</svelte:head>

<script>
    // Import global styles here
    import "../global.css"
</script>

<main class="flex">
    <h1 class="bold">Welcome to <span class="accent">SvelteKit</span></h1>
    <p>Visit <a href="https://kit.svelte.dev" target="_blank" rel="noreferrer">kit.svelte.dev</a> to read the documentation</p>
    <a href="/gpt">Start now</a>
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
            > a {
                color: var(--accent-color);
                font-size: inherit;
                text-decoration: none;
            }

            + a {
                margin-top: 2rem;
                font-size: var(--fs-large);
                color: var(--text-color);
            }
        }
    }
</style>