<script>
	import { LayerCake, Svg } from 'layercake';
	import { timeParse } from 'd3-time-format'; 
	import { scaleSqrt, scaleTime } from 'd3-scale';

	import AxisX from './_components/AxisX.svelte';
	import AxisY from './_components/AxisY.svelte';
	import Dot from './_components/Dot.svelte';

	import strikes from './_data/final_data.csv';

	const parseDate = timeParse("%Y-%m-%d");

	strikes.forEach(row => {
		row['month'] = +row['month'];
		row['n_strikes'] = +row['n_strikes'];
		row['date'] = parseDate(row['date']);
	});

	const xKey = 'date';
	const zKey = 'n_strikes';
</script>

<h1>Russia's increasing air and drone strikes in Ukraine</h1>
<h2>Number of reported air and drone strikes, Jan 1 - Nov 22, 2024</h2>
<div class="chart-container">
	<LayerCake
		padding={{ right: 10, bottom: 20, left: 25 }}
		x={xKey}
		xScale={scaleTime()}
		xDomain={[new Date(2023, 12, 1), new Date(2024, 10, 1)]}
		z={zKey}
		zScale={scaleSqrt()}
		zRange={[0, 100]}
		data={strikes}
		debug
	>
		<Svg>
			<AxisX />
			<AxisY />
			<Dot />
		</Svg>
	</LayerCake>
</div>

<style>
	.chart-container {
		width: 80%;
		height: 80vh;
		margin: 25px auto;
	}
</style>
