<script>
	import { getContext } from 'svelte';

	const { data, xGet, zGet, zScale, config, height } = getContext('LayerCake');
</script>

{#each $data as d}
    <circle
        cx="{$xGet(d)}"
        cy="{$height/2}"
        r="{$zGet(d)}"
    ></circle>
{/each}

<style>
	circle {
		stroke: #000;
		stroke-width: 1px;
		opacity: 0.5;
	}
</style>