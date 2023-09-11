<svelte:head>
	<title>Home page</title>
</svelte:head>

<script>
    // Import global styles here
    import "../../global.css"
    import OpenAI from "openai";
    import { PUBLIC_OPENAI_API_KEY } from "$env/static/public"

    $ : query = "";
    $ : output = "";
    $ : history = [] ;

    const openai = new OpenAI({
        apiKey: PUBLIC_OPENAI_API_KEY,
        dangerouslyAllowBrowser: true
    });

    const openaiSearch = async(query) => {
        let chatCompletion;

        if(history.length > 0) {
            chatCompletion = await openai.chat.completions.create({
                messages: [...history, { role: "user", content: query }],
                model: "gpt-3.5-turbo",
            });
        } else {
            chatCompletion = await openai.chat.completions.create({
                messages: [{ role: "user", content: query }],
                model: "gpt-3.5-turbo",
            });
        }

        history.push({
            role: "user",
            content: query,
        });

        output = chatCompletion.choices[0].message;
        history.push({
            role: output.role,
            content: output.content,
        });

        // Put history in local storage
        localStorage.setItem("history", JSON.stringify(history));

        console.log(history);
        return output
    }

	const handleClick = () => {
        console.log(query)
        openaiSearch(query);
    };



</script>

<main class="flex">
    <h1 class="bold">Let's start <span class="accent">Chatting</span> using AI</h1>

    <section id="chat">

        <section class="history">
            {#each history as message}
            <p class="message {message.role}"> {message.content} </p>
        {/each}

        </section>

        <p class="output"> {output.content} </p>
        <input type="text" name="name" placeholder="Enter your name" bind:value={query}/>
        <button on:click={handleClick}>
            Start Chatting
        </button>
    </section>

</main>

<style lang="scss">
    main {
        height: 100%;
        width: 100%;
        flex-direction: column;
        text-align: center;
        background: #2c3e50;
        color: #fff;

        p {
            margin: 0.5rem;
            font-size: var(--fs-large);
            > a {
                color: var(--accent-color);
                font-size: inherit;
                text-decoration: none;
            }
        }

        #chat {
            margin-top: 1rem;
            width: 60vw;
            padding: 2rem;
            background: #ecf0f1;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            border-radius: 8px;

            input {
                margin-bottom: 1rem;
                padding: 1rem 1.2rem;
                border-radius: 4px;
                border: none;
                outline: none;
                width: 100%;
            }

            .history {
                padding: 1rem 1.2rem;
                border-radius: 4px;
                border: none;
                outline: none;
                width: 100%;
                color: #333;
                font-size: 0.75rem;
            }

            .output {
                margin-bottom: 1rem;
                padding: 1rem 1.2rem;
                border-radius: 4px;
                border: none;
                outline: none;
                width: 100%;
                color: #333;
            }

            button {
                width: 100%;
                padding: .7rem;
                border-radius: 4px;
                border: none;
                outline: none;
                width: 100%;
                background: #333;
                color: #fff;
            }
        }
    }
</style>