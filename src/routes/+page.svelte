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

		if (stage === 'night' || stage ==='evening') {
			document.body.classList.add('dark-theme');
		}

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
		};
		toggle.addEventListener('click', toggleTheme);
	});
</script>

<div class="container">
	<div class="grid">
		<p class="centered row one"><strong>when</strong></p>
		<p class="row one indented">
			it's <span id="time">--:--</span> on a <span id="themeToggle">bright &#10059;</span><br />
			<span id="day">-------</span>, and
		</p>

		<p class="centered row two"><strong>where</strong></p>
		<p class="row two indented">
			you've stumbled upon <a href="/">matthewjl.xyz</a>,<br />
			the personal website belonging to
		</p>

		<p class="centered row three"><strong>who</strong></p>
		<div class="row indented">
			<h1>matthew j lee</h1>
			<br />
			<div class="row three">whose online presence is expressed through</div>
		</div>

		<p class="centered row four"><strong>what</strong></p>
		<div class="split-cell indented" indented>
			<div class="row four">
				<h2><a href="/blog">writing</a></h2>
				<h2><a href="/" on:click={() => {showInfo = true}}>info</a></h2>
				<h2><a href="/portfolio">portfolio</a></h2>
				<h2><a href="/resume">resume</a></h2>
				<h2><a href="/thoughts">thoughts</a></h2>
				<h2><a href="/media">media</a></h2>
			</div>
			<div class="image-wrapper row zero">
				<img src="/images/gingko.png" alt="3 gingko leaves" />
			</div>
		</div>

		<p class="centered row five"><strong>why</strong></p>
		<p class="row five indented">
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
		grid-template-columns: minmax(2rem, 2fr) 3fr minmax(2rem, 2fr);
		width: 100%;
		gap: 0.4rem;
	}

	.row {
		opacity: 0;
		animation: fadein 1s ease-in-out forwards;
	}

	.one {
		animation-delay: 0.6s;
	}

	.two {
		margin-bottom: 1rem;
		animation-delay: 0.8s;
	}

	.three {
		animation-delay: 1s;
	}

	.four {
		animation-delay: 1.2s;
	}

	.five {
		animation-delay: 1.4s;
	}

	h1 {
		font-size: 4rem;
		line-height: 4rem;
		color: var(--color-highlight);
	}

	h1, h2 {
		margin: 0;
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
		display: flex;
		margin-top: 12px;
		width: 100%;
	}

	.image-wrapper {
		max-width: 50%;
		display: flex;
		align-items: center;
	}

	.image-wrapper img {
		width: auto;
		height: auto;
		max-height: 10.5rem;
		max-width: 100%;
		margin-left: 0.8rem;
	}

	.centered {
		text-align: center;
	}

	.right-column {
		grid-column: 3;
		grid-row: 1 / 6;
	}

	.indented {
		margin-left: 25%;
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
