<script>
	import { onMount } from 'svelte';
	import Info from './Info.svelte';
	const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
	let showInfo = false;

	onMount(() => {
		const timeSpan = document.querySelector('#time');
		const daySpan = document.querySelector('#day');

		const now = new Date();

		let hours = now.getHours();
		let stage = 'night';
		if (hours > 4) stage = 'morning';
		if (hours > 12) stage = 'afternoon';
		if (hours > 17) stage = 'evening';

		daySpan.innerHTML = dayNames[now.getDay()] + ' ' + stage;

		let period = hours >= 12 ? 'p.m.' : 'a.m.';

		hours = hours % 12;
		hours = hours ? hours : 12;
		hours = (hours < 10 ? '0' : '') + hours;

		let minutes = now.getMinutes();
		minutes = (minutes < 10 ? '0' : '') + minutes;

		timeSpan.innerHTML = hours + ':' + minutes + period;

		const toggle = document.querySelector('#themeToggle');
		if (document.body.classList.contains('dark-theme')) {
			toggle.innerHTML = 'dark &#10059;'
		}
		const toggleTheme = () => {
			const dim = document.body.classList.toggle('dark-theme');
			toggle.innerHTML = dim ? 'dark &#10059;' : 'bright &#10059;';
			localStorage.setItem("theme", dim ? "dark" : "bright");
		};
		toggle.addEventListener('click', toggleTheme);
	});
</script>

<div class="container">
	<div class="grid">
		<p class="row one"><strong>when</strong></p>
		<p class="row one text-right">
			it's <span id="time">--:--</span> on a <span id="themeToggle">bright &#10059;</span><br />
			<span id="day">------- --------</span>, and
		</p>

		<p class="row two"><strong>where</strong></p>
		<p class="row two text-right">
			you've stumbled upon <a href="/">matthewjl.xyz</a>,<br />
			the personal website belonging to
		</p>

		<p class="row three"><strong>who</strong></p>
		<div class="row text-right">
			<h1>matthew j lee</h1>
			<br />
			<div class="row three">whose online presence is expressed through</div>
		</div>

		<p class="row four"><strong>what</strong></p>
		<div class="split-cell">
			<div class="image-wrapper row zero">
				<img src="/images/gingko.png" alt="3 gingko leaves" />
			</div>
			<div class="row four text-right">
				<h2><a href="https://fieldnotes.matthewjl.xyz">writing</a></h2>
				<h2><a href="/" on:click={() => {showInfo = true}}>info</a></h2>
				<h2><a href="https://portfolio.matthewjl.xyz">portfolio</a></h2>
				<h2><a href="/thoughts">thoughts</a></h2>
				<h2><a href="/media">media</a></h2>
			</div>
		</div>

		<p class="row five"><strong>why</strong></p>
		<p class="row five text-right">
			in the hope of<br />
			maintaining a personal record,<br />
			connecting from afar,<br />
			nurturing a personal space,<br />
			& learning/creating continuously.
		</p>

		<div class="right-column" />
	</div>
	{#if showInfo}
		<Info on:close={() => {showInfo = false;}}/>
	{/if}

</div>

<style>
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.grid {
		display: grid;
		grid-template-columns: min-content 1fr;
		width: 100%;
		gap: 0.2rem;
		max-width: 600px;
	}

	.row {
		opacity: 0;
		animation-iteration-count: 1 !important;
		animation: fadein 1s ease-in-out forwards;
	}

	.one {
		animation-delay: 0.4s;
	}

	.two {
		margin-bottom: 1rem;
		animation-delay: 0.5s;
	}

	.three {
		animation-delay: 0.6s;
	}

	.four {
		animation-delay: 0.7s;
	}

	.five {
		animation-delay: 0.8s;
	}

	h1 {
		font-size: 4rem;
		line-height: 4rem;
		color: var(--color-highlight);
	}

	h1, h2 {
		margin: 0.2rem 0;
	}

	p {
		margin-bottom: 0.2em;
	}

	strong {
		font-family: 'Nanum Myeongjo ExtraBold';
		color: var(--color-accent);
		opacity: 0.8;
	}

	.split-cell {
		margin-top: 12px;
		margin-left: auto;
		display: flex;
	}

	.row.four {
		width: fit-content;
	}
	.image-wrapper {
		padding: 1em;
	}

	.image-wrapper img {
		width: 8.8em;
		height: 8.8em;
	}

	.right-column {
		grid-column: 3;
		grid-row: 1 / 6;
	}

	.text-right {
		text-align: right;
	}

	#themeToggle {
		color: var(--color-accent);
		cursor: pointer;
	}

	@keyframes fadein {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
</style>
