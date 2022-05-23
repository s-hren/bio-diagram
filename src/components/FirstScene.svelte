<script>
	import { CircleBufferGeometry, MeshStandardMaterial, BoxBufferGeometry, DoubleSide } from 'three';
	import { DEG2RAD } from 'three/src/math/MathUtils';
	import {
		AmbientLight,
		Canvas,
		DirectionalLight,
		Group,
		HemisphereLight,
		Mesh,
		OrbitControls,
		PerspectiveCamera
	} from 'threlte';
	import { spring } from 'svelte/motion';
	import Donut from './Donut.svelte';
	import { createEventDispatcher } from 'svelte';

	const scale = spring(1);

	const dispatch = createEventDispatcher();

	const forward = (e, clicked) => {
		dispatch('canvas-click', clicked);
	};
</script>

<div class="wrapper">
	<Canvas
		on:click-canvas={(e) => {
			forward(e, e.detail);
		}}
	>
		<Donut on:hover-donut />
		<PerspectiveCamera position={{ x: 10, y: 10, z: 10 }} fov={24}>
			<OrbitControls autoRotate={false} enableZoom={false} target={{ y: 0.5 }} />
		</PerspectiveCamera>

		<DirectionalLight shadow position={{ x: 3, y: 10, z: 10 }} />
		<DirectionalLight shadow position={{ x: 0, y: -5, z: -5 }} />
		<DirectionalLight position={{ x: -3, y: 10, z: -10 }} intensity={0.2} />
		<AmbientLight intensity={0.2} />

		<!-- Cube -->
		<!-- <Group scale={$scale}>
			<Mesh
				interactive
				on:pointerenter={() => ($scale = 2)}
				on:pointerleave={() => ($scale = 1)}
				position={{ y: 0.5 }}
				castShadow
				geometry={new BoxBufferGeometry(1, 1, 1)}
				material={new MeshStandardMaterial({ color: '#333333' })}
			/>
		</Group> -->

		<!-- Floor -->
		<!-- <Mesh
			receiveShadow
			rotation={{ x: -90 * (Math.PI / 180) }}
			geometry={new CircleBufferGeometry(3, 72)}
			material={new MeshStandardMaterial({ side: DoubleSide, color: 'white' })}
		/> -->
	</Canvas>
</div>

<style>
	.wrapper {
		height: 100vh;
		width: 100vw;
		max-width: 100vw;
		border: black 1px solid;
	}
</style>
