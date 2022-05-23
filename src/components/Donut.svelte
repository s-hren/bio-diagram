<script>
	import { GLTF } from 'threlte';
	import { spring } from 'svelte/motion';
	import { createEventDispatcher } from 'svelte';

	let scale = spring(40);

	const dispatch = createEventDispatcher();

	const forward = (e, entered) => {
		dispatch('hover-donut', entered);
	};
</script>

<GLTF
	url={'/donuta.glb'}
	scale={$scale}
	interactive
	castShadow
	on:pointerenter={(e) => forward(e, true)}
	on:pointerleave={(e) => forward(e, false)}
	on:click={() => {
		console.log('User clicked!');
	}}
/>
