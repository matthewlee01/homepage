<script>
	import { onMount } from 'svelte';
	const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

	onMount(() => {
		const timeSpan = document.querySelector('#time');
		const daySpan = document.querySelector('#day');

		const now = new Date();

		let hours = now.getHours();
		let stage = 'night';
		if (hours > 5) stage = 'morning';
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
	});
</script>

<div class="container">
	<div class="grid">

		<p class="centered row one"><strong>when</strong></p>
		<p class="row one indented">
			it's <span id="time">--:--</span><br />
			on a <span id="day">-------</span>, and
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
				<h2><a href="/">writing</a></h2>
				<h2><a href="/">work</a></h2>
				<h2><a href="/">credentials</a></h2>
				<h2><a href="/">opinions</a></h2>
				<h2><a href="/">thoughts</a></h2>
				<h2><a href="/">personal info</a></h2>
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

		<div class="right-column"></div>

	</div>
</div>

<style>
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.grid {
		display: grid;
		grid-template-columns: 0.8fr 1fr minmax(0px, 0.6fr);
		width: 100%;
		gap: 0.4rem;
	}

	.row {
		opacity: 0;
		animation: fadein 1s ease-in-out forwards;
	}

	.one {
		animation-delay: 0.8s
	}

	.two {
		animation-delay: 1.2s
	}

	.three {
		animation-delay: 1.6s
	}

	.four {
		animation-delay: 2s
	}

	.five {
		animation-delay: 2.4s
	}
	
	
	
	h1 {
		font-size: 4rem;
		line-height: 4rem;
		color: var(--sinopia);
	}

	p {
		margin-bottom: 0.2em;
	}

	strong {
		font-family: 'Nanum Myeongjo ExtraBold';
		color: var(--moonstone);
		opacity: 0.5;
	}

	.split-cell {
		display: flex;
		margin-top: 12px;
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
	}

	.centered {
		text-align: center;
	}

	.right-column {
		grid-column: 3;
		grid-row: 1 / 5;
	}

	.indented {
		margin-left: 12%;
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
