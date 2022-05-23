<script>
	import FirstScene from '../components/FirstScene.svelte';

	let display = 'none';

	let donutHovered = false;

	var pointerX = -1;
	var pointerY = -1;

	let isMouseDown = false;

	const followMouse = (e) => {
		pointerX = e.clientX + 5;
		pointerY = e.clientY + 5;
		console.log(pointerX, pointerY);
	};

	const hoverDonut = (e) => {
		if (e.detail === true) {
			if (!isMouseDown) {
				display = 'inline';
			}
			console.log('Donut hovered!');
			donutHovered = true;
		} else {
			console.log('Donut left!');
			display = 'none';
			donutHovered = false;
		}
	};

	const canvasClick = (e, detail) => {
		if (e.detail === true) {
			console.log('Canvas clicked!');
			isMouseDown = true;
			display = 'none';
		} else {
			console.log('Canvas left!');
			isMouseDown = false;
			if (donutHovered) {
				display = 'inline';
			}
		}
	};
</script>

<svelte:window on:mousemove={followMouse} />

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<FirstScene on:hover-donut={hoverDonut} on:canvas-click={canvasClick} />

<div class="tooltip" style="display: {display}; top: {pointerY}px; left: {pointerX}px;">Donut</div>

<style>
	.tooltip {
		position: absolute;
		background: rgba(0, 0, 0, 0.5);
		color: white;
		height: fit-content;
		text-align: center;
		font-size: 2em;
		z-index: 5;
	}
</style>
