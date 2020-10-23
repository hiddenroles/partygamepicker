<script>
	import 'bulma/css/bulma.css'
	import '@fortawesome/fontawesome-free/css/all.css'
	import Games from './games';

	const shuffleGame = () => {
		gameMessage = "[...]"
		setTimeout(() => {
			gameMessage = "[shuffling dices...]";
			setTimeout(() => {
				gameMessage = "[rolling cards...]";
				setTimeout(() => {
					chosenGame = true;
					game = Games.GamesList[Math.floor(Math.random() * Games.GamesList.length)]
					gameMessage = game["name"]
				}, 1500)
			}, 1500)
		}, 1500)
	}

	let game = null;
	let settings = false;
	let gameMessage = "...";
	let chosenGame = false;

	// onMount(() => {
	// 	shuffleGame()
	// });
</script>

<a class="github-fork-ribbon" href="https://github.com/marcolussetti/partygamepicker" data-ribbon="Fork me on GitHub" title="Fork me on GitHub">Fork me on GitHub</a>
<section class="hero is-light is-fullheight">
    <div class="hero-body">
        <div class="container">
            <h1 class="title">
                We are playing <i>{gameMessage}</i>
            </h1>
            {#if game}
                <div class="box">
					<div class="container">
                        <h1 class="subtitle has-text-centered is-italic"><p><a href="{game.url}">{game.name}</a></p></h1>
					</div>
                    <div class="columns">
                        <div class="column">
                            <nav class="panel">
                                <div class="panel-block">
                                    <div class="container is-fluid">
                                        <div class="columns">
                                            <div class="column is-one-third has-text-weight-bold">Min Players:</div>
                                            <div class="column is-two-thirds">{game.min_players}</div>
                                        </div>
                                    </div>
                                </div>

                                <div class="panel-block">
                                    <div class="container is-fluid">
                                        <div class="columns">
                                            <div class="column is-one-third has-text-weight-bold">Max Players:</div>
                                            <div class="column is-two-thirds">{game.max_players}</div>
                                        </div>
                                    </div>
                                </div>
                            </nav>
                        </div>

                        <div class="column">
                            <nav class="panel">
                                <div class="panel-block">
                                    <div class="container is-fluid">
                                        <div class="columns">
                                            <div class="column is-one-third has-text-weight-bold">Requires:</div>
                                            <div class="column is-two-thirds">{game.requires}</div>
                                        </div>
                                    </div>
                                </div>

                                <div class="panel-block">
                                    <div class="container is-fluid">
                                        <div class="columns">
                                            <div class="column is-one-third has-text-weight-bold">Requires streaming:
                                            </div>
                                            <div class="column is-two-thirds">{game.requires_streaming ? "yes" : "no"}</div>
                                        </div>
                                    </div>
                                </div>
                            </nav>
                        </div>
                    </div>
                </div>
            {/if}

            <button on:click={() => shuffleGame()}>
                {#if chosenGame}
                    Thx I hate it
                {:else}
                    Give me a game
                {/if}
            </button>
        </div>
    </div>
</section>
