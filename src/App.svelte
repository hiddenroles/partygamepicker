<script>
	import 'bulma/css/bulma.css'
	// import 'bulma-slider/dist/bulma-slider.mind.css'
	import '@creativebulma/bulma-collapsible/dist/css/bulma-collapsible.min.css';
	import '@fortawesome/fontawesome-free/css/all.css'
	import Games from './games';
	// import * as bulmaSlider from "bulma-slider";
	// import * as bulmaSlider from 'bulma-slider/dist/js/bulma-slider.min.js'

	const shuffleGame = () => {
		gameMessage = "[...]"
		game = null
		setTimeout(() => {
			gameMessage = "[shuffling dices...]";
			setTimeout(() => {
				gameMessage = "[rolling cards...]";
				setTimeout(() => {
					chosenGame = true;
					game = pickGame(Games.GamesList, settings)
					gameMessage = game["name"]
				}, 1500)
			}, 1500)
		}, 1500)
	}

	let game = null;
	let settingsShown = true;
	let gameMessage = "...";
	let chosenGame = false;
	let pickerMode = true;

	let settings = {
		"sliders": {
			"players": {
				"enabled": false,
				"value": 5
			},
			"cost": {
				"enabled": false,
				"value": 10
			},
		},
		"requirements": {
			"streaming": true,
			"steam": true,
			"windows": true,
			"mac": true,
			"ios": true,
			"android": true,
			"linux": true
		}
	}

	// onMount(() => {
	// 	shuffleGame()
	// });
	// bulmaSlider.attach();

	function toggleSettings(e) {
		e.stopPropagation()
		console.log('Toggling settings')
		settingsShown = !settingsShown
	}

	function togglePicker(e) {
		e.stopPropagation()
		console.log('Toggling mode')
		pickerMode = !pickerMode
	}

	function toggleSlider(filter, e) {
		console.log(`Toggling slider ${filter} to ${e.target.value}`)
		settings.sliders[filter].enabled = e.target.checked
	}

	function pickGame(games, settings) {
		if (settings.sliders.players.enabled) {
			games = games.filter(game => {
				return game.max_players >= settings.sliders.players.value && game.min_players <= settings.sliders.players.value
			})
		}
		// if (settings.sliders.cost.enabled) {
		// 	games = games.filter(game => {
		// 		return game.cost <= settings.sliders.cost.value
		// 	})
		// }

		// console.log(games);

		return games[Math.floor(Math.random() * games.length)]
	}
</script>

<style>
	.slider {
		width: 100%;
	}

	.filters, .game-card {
		transition: visibility 0.2s ease-in-out, opacity 0.2s ease-in-out;
	}

	.is-disabled-slider {
		color: darkgray;
	}

	.is-disabled-slider:hover {
		color: darkgray !important;
	}

	.is-inactive {
		opacity: 0;
		visibility: hidden;
	}

	.is-sticky-filter {
		position: fixed;
		top: 45vh;
	}

</style>

<!--<svelte:head>-->
<!--	<script defer src='https://cdn.jsdelivr.net/npm/bulma-slider@2.0.4/dist/js/bulma-slider.min.js' on:load={bulmaSlider.attach()}></script>-->
<!--</svelte:head>-->

<a class="github-fork-ribbon" data-ribbon="Fork me on GitHub" href="https://github.com/hiddenroles/partygamepicker"
	 title="Fork me on GitHub">Fork me on GitHub</a>
<nav aria-label="main navigation" class="navbar" role="navigation">
	<div class="navbar-brand">
		<a class="navbar-item" href="https://hiddenroles.com">
			<img alt="HiddenRoles" height="28" src="hiddenroles.png">
		</a>

		<a aria-expanded="false" aria-label="menu" class="navbar-burger burger" data-target="navbarBasicExample"
			 role="button">
			<span aria-hidden="true"></span>
			<span aria-hidden="true"></span>
			<span aria-hidden="true"></span>
		</a>
	</div>

	<div class="navbar-menu" id="navbarBasicExample">
		<div class="navbar-start">
			<a class="navbar-item" href="/">
				PartyGamePicker
			</a>

			<a class="navbar-item" on:click={toggleSettings}>
				{settingsShown ? "Hide filters" : "Show filters"}
			</a>

			<a class="navbar-item" on:click={togglePicker}>
				{pickerMode ? "Switch to all games" : "Switch to picker"}
			</a>
		</div>
	</div>
</nav>
<section class="hero is-light is-fullheight-with-navbar">
	<div class="hero-body columns">
		<div class="column is-one-quarter">
			<div class="filters card {!settingsShown ? 'is-inactive' : ''} {!pickerMode ? 'is-sticky-filter' : ''}">
				<header class="card-header">
					<p class="card-header-title">
						Filters
					</p>
				</header>

				<div class="is-collapsible">
					<div class="card-content">
						<div class="title is-5 columns">
							<div class="column">
								<label class="checkbox {!settings.sliders.players.enabled ? 'is-disabled-slider': ''}">
									<input on:change="{e => toggleSlider('players', e)}" type="checkbox"
												 value={settings.sliders.players.enabled}>
									Players
								</label>
							</div>
							<div class="column">
								<input class="slider is-fullwidth is-circle" disabled={!settings.sliders.players.enabled}
											 id="playersCountSlider" max="20"
											 min="1"
											 on:change="{e => settings.sliders.players.value = e.target.value}" step="1" type="range"
											 value={settings.sliders.players.value}>
							</div>
							<div class="column">
								<label class="has-text-centered {!settings.sliders.players.enabled ? 'is-disabled-slider': ''}"
											 for="playersCountSlider">{settings.sliders.players.value}</label>
							</div>
						</div>

						<!--						<div class="title is-5 columns">-->
						<!--							<div class="column">-->
						<!--								<label class="checkbox  {!settings.sliders.cost.enabled ? 'is-disabled-slider': ''}"-->
						<!--											 on:click="{e => toggleSlider('cost', e)}">-->
						<!--									<input type="checkbox" value={settings.sliders.cost.enabled}>-->
						<!--									Cost-->
						<!--								</label>-->
						<!--							</div>-->
						<!--							<div class="column">-->
						<!--								<input class="slider has-output-tooltip is-fullwidth" disabled={!settings.sliders.cost.enabled} id="costSlider" max="20"-->
						<!--											 min="1"-->
						<!--											 on:change="{e => settings.sliders.cost.value = e.target.value}" step="1" type="range"-->
						<!--											 value={settings.sliders.cost.value}>-->
						<!--							</div>-->
						<!--							<div class="column">-->
						<!--								<label class="has-text-centered {!settings.sliders.cost.enabled ? 'is-disabled-slider': ''}"-->
						<!--											 for="playersCountSlider">{"<"}{settings.sliders.cost.value}$</label>-->
						<!--							</div>-->
						<!--						</div>-->

					</div>
				</div>

			</div>

		</div>
		<div class="column is-three-quarters">
			{#if pickerMode}
				<div class="container">
					<h1 class="title">
						We are playing <i>{gameMessage}</i>
					</h1>
					<div class="box game-card {!game ? 'is-inactive': ''}">
						<div class="container">
							<h1 class="subtitle has-text-centered is-italic"><p><a
								href="{game ? game.url: ''}">{game ? game.name : ''}</a></p></h1>
						</div>
						<div class="columns">
							<div class="column">
								<nav class="panel">
									<div class="panel-block">
										<div class="container is-fluid">
											<div class="columns">
												<div class="column is-one-third has-text-weight-bold">Min Players:</div>
												<div class="column is-two-thirds">{game ? game.min_players : ''}</div>
											</div>
										</div>
									</div>

									<div class="panel-block">
										<div class="container is-fluid">
											<div class="columns">
												<div class="column is-one-third has-text-weight-bold">Max Players:</div>
												<div class="column is-two-thirds">{game ? game.max_players : ''}</div>
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
												<div class="column is-two-thirds">{game ? game.requires : ''}</div>
											</div>
										</div>
									</div>

									<div class="panel-block">
										<div class="container is-fluid">
											<div class="columns">
												<div class="column is-one-third has-text-weight-bold">Requires streaming:
												</div>
												<div class="column is-two-thirds">{game ? game.requires_streaming ? "yes" : "no" : ''}</div>
											</div>
										</div>
									</div>
								</nav>
							</div>
						</div>
					</div>

					<button on:click={() => shuffleGame()}>
						{#if chosenGame}
							Thx I hate it
						{:else}
							Give me a game
						{/if}
					</button>
				</div>
			{:else}
				<div class="container">
					{#each Games.GamesList.filter(g => {
						return settings.sliders.players.enabled ? g.max_players >= settings.sliders.players.value && g.min_players <= settings.sliders.players.value : true
					}) as gameEl}
						<div class="box">
							<div class="container">
								<h1 class="subtitle has-text-centered is-italic"><p><a href="{gameEl.url}">{gameEl.name}</a></p></h1>
							</div>
							<div class="columns">
								<div class="column">
									<nav class="panel">
										<div class="panel-block">
											<div class="container is-fluid">
												<div class="columns">
													<div class="column is-one-third has-text-weight-bold">Min Players:</div>
													<div class="column is-two-thirds">{gameEl.min_players}</div>
												</div>
											</div>
										</div>

										<div class="panel-block">
											<div class="container is-fluid">
												<div class="columns">
													<div class="column is-one-third has-text-weight-bold">Max Players:</div>
													<div class="column is-two-thirds">{gameEl.max_players}</div>
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
													<div class="column is-two-thirds">{gameEl.requires}</div>
												</div>
											</div>
										</div>

										<div class="panel-block">
											<div class="container is-fluid">
												<div class="columns">
													<div class="column is-one-third has-text-weight-bold">Requires streaming:
													</div>
													<div class="column is-two-thirds">{gameEl.requires_streaming ? "yes" : "no"}</div>
												</div>
											</div>
										</div>
									</nav>
								</div>
							</div>
						</div>
					{/each}
				</div>
			{/if}
		</div>
	</div>
</section>
