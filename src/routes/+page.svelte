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

		hours = hours % 12;
		hours = (hours < 10 ? '0' : '') + hours;

		let minutes = now.getMinutes();
		minutes = (minutes < 10 ? '0' : '') + minutes;

		let period = hours / 12 > 1 ? 'p.m.' : 'a.m.';

		timeSpan.innerHTML = hours + ':' + minutes + period;
	});
</script>

<div class="container">
	<div class="qna">
		<p class="right"><strong>when</strong></p>
		<p id="when">
			it's <span id="time">--:--</span><br />
			on a <span id="day">------</span>, and
		</p>
		<p class="right"><strong>where</strong></p>
		<p>
			you've stumbled upon <a href="/">matthewjl.xyz</a>,<br />
			the personal website belonging to
		</p>
		<p class="right"><strong>who</strong></p>
		<div>
			<h1>matthew j lee</h1>
			<br />
			whose online presence is expressed through
		</div>
		<p class="right"><strong>what</strong></p>
		<div class="split-cell">
			<div>
				<h2><a href="/">writing</a></h2>
				<h2><a href="/">work</a></h2>
				<h2><a href="/">credentials</a></h2>
				<h2><a href="/">opinions</a></h2>
				<h2><a href="/">thoughts</a></h2>
				<h2><a href="/">personal info</a></h2>
			</div>
			<div class="image-wrapper">
				<img src="/images/gingko.png" alt="3 gingko leaves" />
			</div>
		</div>
		<p class="right"><strong>why</strong></p>
		<p>
			in the hope of<br />
			maintaining a personal record,<br />
			connecting from afar,<br />
			nurturing a personal space,<br />
			& learning/creating continuously.
		</p>
	</div>
</div>

<style>
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.qna {
		display: grid;
		grid-template-columns: 1fr 7.2fr;
		width: 100%;
		max-width: 720px;
		gap: 0.8rem 20%;
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

	.right {
		text-align: right;
	}
	
</style>
