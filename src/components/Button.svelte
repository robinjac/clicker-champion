<script lang="ts">
	import { onMount, getContext } from "svelte";
	import { tweened } from "svelte/motion";
	import { cubicOut, linear, cubicInOut } from 'svelte/easing';

	export let x = 0;
	export let y = 0;

	$: X = tweened(x, {
		duration: 500,
		easing: cubicOut
	});

	$: Y = tweened(y, {
		duration: 500,
		easing: cubicOut
	});

	const rotation = tweened(0, {
		duration: 2000,
		easing: linear
	});

	const scale = tweened(1, {
		duration: 100,
		easing: cubicInOut
	});

	const width = getContext<SvelteStore<number>>("canvasWidth");
	const height = getContext<SvelteStore<number>>("canvasHeight");

	let count = 0;
	let element;
	let clicked = false;
	let timeout;

	async function update(){
		await Promise.all([X.set(Math.random()*($width - 80)), Y.set(Math.random()*($height - 40))]);
		if(!clicked){
			timeout = setTimeout(update, 500);
		}
	}

	function mouseDown() {
		clearTimeout(timeout);
		$scale = 0.85;
		count += 1;
		clicked = true;
	}

	function mouseUp() {
		$scale = 1;
		clicked = false;
		timeout = setTimeout(update, 500);
	}

	onMount(update);

</script>

<button style="transform: translate({$X - 40}px, {$Y - 20}px) scale({$scale}) rotate({$rotation}deg);" bind:this={element} on:mousedown|preventDefault={mouseDown} on:mouseup|preventDefault={mouseUp}>click me</button>

<style type="text/scss">

	button {
		height: 40px;
		width: 80px;
		border: 1px solid rgb(255, 4, 242);
		border-radius: 4px;
		outline: none;
		background-color: rgb(118, 5, 170);
		color: white;
		cursor: pointer;
		transition: box-shadow 0.2s ease-in-out;
		user-select: none;
		
		&:hover {
			box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
		}

		&:active {
			transition: transform 0.1s ease-in-out;
			background-color: rgb(118, 5, 170);
		}
	}
</style>