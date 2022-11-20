<script>
	import { onMount } from 'svelte';

	const gamesInfo = [
		{
			user: 'mattmora',
			game: 'stellata-waterway'
		},
		{
			user: 'mattmora',
			game: 'an-autumn-day'
		},
		{
			user: 'mattmora',
			game: 'the-harrowing-life-of-the-violet-snail'
		}
	];

	let games = [];

	onMount(async () => {
		gamesInfo.forEach((info) => {
			Itch.getGameData({
				...info,
				onComplete: (data) => {
					data.url = `https://${info.user}.itch.io/${info.game}`;
					games = [...games, data];
					console.log(data);
				}
			});
		});
	});
</script>

<svelte:head>
	<script type="text/javascript" src="https://static.itch.io/api.js"></script>
</svelte:head>

<div class="content">
	<header>
		<!-- <div class="navigation" /> -->
		<div class="block">
			<h1 id="name">Matt Wang</h1>
			<h5 id="aka">aka mattmora</h5>
			<h2 id="roles">Game Designer & Developer</h2>
			<a href="https://mattmora.itch.io">mattmora.itch.io</a>
		</div>
	</header>
	<main>
		<div class="block">
			<p>Hi! Thanks for coming to my site.</p>
			<p>It's a work in progress.</p>
		</div>
		<div class="games">
			{#each games as game}
				<figure>
					<img src={game.cover_image} alt="{game.title} cover image" />
					<figcaption>{game.title}</figcaption>
				</figure>
			{/each}
		</div>
	</main>
</div>

<style>
	.content {
		width: fit-content;
		margin: 0;
		margin-top: 1em;
		position: absolute;
		top: 50%;
		left: 50%;
		-ms-transform: translate(max(-50%, -50vw), max(-200%, -50vh));
		transform: translate(max(-50%, -50vw), max(-200%, -50vh));
	}

	header {
	}

	main {
	}

	.block {
		margin-bottom: 1em;
		padding: 2em;
		background-color: var(--background);
		border: 10px ridge var(--text-faded);
	}

	.games {
		display: grid;
		grid-template-columns: calc(50% - 0.5em) calc(50% - 0.5em);
		column-gap: 1em;
		row-gap: 1em;
	}

	figure {
		display: flex;
		flex-flow: column;
		width: fit-content;
		margin: 0;
		border: 10px ridge var(--text-faded);
	}

	img {
		width: 100%;
		/* max-width: 200px; */
	}

	figcaption {
		font-weight: bold;
		width: calc(100% - 0.5em);
		height: calc(100% - 0.5em);
		padding: 0.25em;
		background-color: var(--text-faded);
		text-align: center;
	}

	#name {
		color: var(--text-primary);
		text-shadow: -0.04em 0 var(--accent);
		margin: 0;
		margin-bottom: 0.2em;
		line-height: 0.8em;
	}

	#aka {
		margin: 0;
		margin-top: -1em;
		color: var(--text-faded);
	}

	#roles {
		color: var(--text-faded);
		margin-top: 0;
		margin-bottom: 0.5em;
		margin-left: -2px;
	}
</style>
