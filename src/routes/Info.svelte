<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	let hiding;

	let close = () => {
		hiding = true;
		setTimeout(() => dispatch('close'), 500);
	};
</script>

<div class:invisible={hiding} class="container">
	<div class="tile-slot tl">
		<div class="tile tl">
			<div class="tile-content">
				<h2>about me</h2>
				<p>
					hi! i'm
					<strong>matthew</strong>, a 4th year student studying Computer Science
					at UBC.<br />
					<br />
					i'm currently interested in front-end design, raccoons, and blogs!<br
					/>
					<br />
					right now, i work part-time at
					<a href="https://pekoproduce.com" target="_blank">peko produce</a>, a
					local grocery delivery which diverts imperfect fruits and veggies from
					the landfill.
				</p>
			</div>
		</div>
	</div>
	<div class="tile-slot tr">
		<div class="tile tr">
			<div class="tile-content">
				<h2>what i'm up to</h2>
				<p>when i'm not at work or in class, you can find me:</p>
				<ul>
					<li>going for a nice long walk</li>
					<li>working on side projects</li>
					<li>reading/writing (very slowly)</li>
					<li>attempting to play sports</li>
					<li>consuming way too much media</li>
					<li>oversleeping / undersleeping / napping</li>
				</ul>
			</div>
		</div>
	</div>
	<div class="tile-slot bl">
		<div class="tile bl">
			<div class="tile-content">
				<h2>socials</h2>
				<p>
					email
					<span
						><a href="mailto:laughew@gmail.com">laughew[at]gmail[dot]com</a
						></span
					><br />
					<br />
					twitter
					<span
						><a href="https://twitter.com/matthew_j_l" target="_blank"
							>@matthew_j_l</a
						></span
					><br />
					<br />
					linkedin
					<span
						><a
							href="https://www.linkedin.com/in/matthew-lee01/"
							target="_blank">matthew-lee01</a
						></span
					><br />
					<br />
					github
					<span
						><a href="https://github.com/matthewlee01" target="_blank"
							>@matthewlee01</a
						></span
					><br />
					<br />
				</p>
			</div>
		</div>
	</div>
	<div class="tile-slot br">
		<div class="tile br">
			<div class="tile-content">
				<button on:click={close}>close</button>
			</div>
		</div>
	</div>
</div>

<style>
	h2 {
		margin: 0;
	}

	ul {
		column-count: 2;
		padding-left: 1rem;
	}

	button {
		border: 2px solid var(--moonstone);
		background-color: var(--burnt-orange);
		padding: 0.4rem 1.6rem;
		font-family: inherit;
		text-shadow: -0.6px -0.6px var(--color-shadow);
		color: inherit;
		cursor: pointer;
		box-shadow: -1px -1px 0px 1px var(--color-shadow),
			inset -1px -1px 0px 1px var(--color-shadow);
	}

	button:hover {
		background-color: var(--floral-white);	
		color: var(--burnt-orange);
	}

	.container {
		display: flex;
		flex-wrap: wrap;
		width: 100%;
		min-height: 100%;
		position: fixed;
		top: 0;
		left: 0;
		transition: 0.5s opacity;
		opacity: 1;
	}

	.invisible {
		opacity: 0;
	}

	.tile-slot {
		width: 50%;
		height: 50%;
		height: 50vh;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	@media only screen and (max-width: 600px) {
		.tile-slot {
			width: 100%;
			height: 30vh;
			font-size: 0.8rem;
		}

		.tile-slot.br {
			height: 10vh;
		}
	}

	.tile {
		width: 100%;
		height: 100%;
		transform-origin: 50% 50%;
		overflow: hidden;
		box-shadow: 0px 0px 16px var(--color-shadow);
		font-family: 'Nanum Myeongjo';
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.tile-content {
		opacity: 0;
		animation: 1s reveal ease forwards;
		text-shadow: -0.4px -0.4px var(--color-shadow);
		margin: 1.2rem;
		gap: 1rem;
		max-width: 320px;
	}

	@keyframes reveal {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	.tl.tile {
		background-color: var(--papaya-whip);
		width: 5%;
		animation: 1s slidein-tl cubic-bezier(0.22, 0.61, 0.36, 1),
			0.4s 1s unfold-tl ease-in-out forwards;
		color: var(--midnight-green);
	}

	.tl .tile-content {
		animation-delay: 1.4s;
	}

	@keyframes slidein-tl {
		from {
			translate: 2000% 100%;
			rotate: 0deg;
		}
		to {
			translate: 0% 0%;
			rotate: -45deg;
		}
	}

	@keyframes unfold-tl {
		0% {
			width: 5%;
			rotate: -45deg;
		}
		100% {
			width: 100%;
			rotate: 0deg;
		}
	}

	.tr.tile {
		background-color: var(--midnight-green);
		height: 5%;
		animation: 1.1s slidein-tr cubic-bezier(0.22, 0.61, 0.36, 1),
			0.4s 1.01s unfold-tr ease-in-out forwards;
		color: var(--papaya-whip);
	}

	.tr .tile-content {
		animation-delay: 1.5s;
	}

	@keyframes slidein-tr {
		from {
			translate: 120% -2400%;
			rotate: 0deg;
		}
		to {
			translate: 0% 0%;
			rotate: -45deg;
		}
	}

	@keyframes unfold-tr {
		0% {
			height: 5%;
			rotate: -45deg;
		}
		100% {
			height: 100%;
			rotate: 0deg;
		}
	}

	.bl.tile {
		background-color: var(--moonstone);
		height: 5%;
		animation: 1.2s slidein-bl cubic-bezier(0.22, 0.61, 0.36, 1),
			0.4s 1.02s unfold-bl ease-in-out forwards;
		color: var(--burnt-orange);
	}

	.bl .tile-content {
		animation-delay: 1.6s;
		width: 100%;
	}

	@keyframes slidein-bl {
		from {
			translate: -140% 2800%;
			rotate: 0deg;
		}
		to {
			translate: 0% 0%;
			rotate: -45deg;
		}
	}

	@keyframes unfold-bl {
		0% {
			height: 5%;
			rotate: -45deg;
		}
		100% {
			height: 100%;
			rotate: 0deg;
		}
	}

	.br.tile {
		background-color: var(--burnt-orange);
		width: 5%;
		animation: 1.3s slidein-br cubic-bezier(0.22, 0.61, 0.36, 1),
			0.4s 1.03s unfold-br ease-in-out forwards;
		color: var(--moonstone);
	}

	.br .tile-content {
		animation-delay: 1.7s;
	}

	@keyframes slidein-br {
		from {
			translate: -100vw -100vh;
			rotate: 0deg;
		}
		to {
			translate: 0% 0%;
			rotate: -45deg;
		}
	}

	@keyframes unfold-br {
		0% {
			width: 5%;
			rotate: -45deg;
		}
		100% {
			width: 100%;
			rotate: 0deg;
		}
	}

	.bl span {
		float: right;
	}
</style>
