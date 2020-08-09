<script lang="ts">
	let count = 0;

	$: console.log("hello there", count);

	function clickHandler(){
		count += 1;
	}

</script>

<button on:click|preventDefault={clickHandler}>click me</button>

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
		align-self: center;
		
		&:hover {
			box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
		}

		&:active {
			background-color: rgb(118, 5, 170);
			transition: transform 0.1s ease-in-out;
			transform: scale(0.95);
		}
	}
</style>