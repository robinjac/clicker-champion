<script lang="ts">
    import { setContext, onMount } from "svelte";
    import { writable } from "svelte/store";
    import Button from "./Button.svelte";

    const height = writable(0);
    const width = writable(0);
    const x = writable(0);
    const y = writable(0);

    let canvas;

    setContext<SvelteStore<number>>("canvasWidth", width);
    setContext<SvelteStore<number>>("canvasHeight", height);

    function onWindowResize() {
        $width = canvas.clientWidth;
        $height = canvas.clientHeight;
    }

    onMount(() => {
        $width = canvas.clientWidth;
        $height = canvas.clientHeight;
        $x = $width / 2;
        $y = $height / 2;
    });

</script>

<svelte:window on:resize={onWindowResize}/>

<div bind:this={canvas}>
    <Button x={$x} y={$y} />
</div>

<style type="text/scss">
    div {
        position: absolute;
        max-width: 75vh;
        max-height: 217vw;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
        background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    }
</style>