<script>
	import { onMount } from "svelte";
	import Chart from "chart.js";
	
	async function renderChart() {

		const res = await fetch("https://pomber.github.io/covid19/timeseries.json");
		const json = await res.json();

		console.log(json);


		var ctx = document.getElementById("myChart").getContext("2d");
		var chart = new Chart(ctx, {
		type: "line",
		data: {
			labels: ["January", "February", "March", "April", "May", "June", "July"],
			datasets: [
			{
				label: "My First dataset",
				backgroundColor: "rgb(255, 99, 132)",
				borderColor: "rgb(255, 99, 132)",
				data: [0, 10, 5, 2, 20, 30, 45]
			}
			]
		},
		options: {}
		});
	}

	onMount(async () => {
		renderChart()
	});

</script>

<main>
	<canvas id="myChart"></canvas>
	<button on:click={renderChart}>Renderr Chart</button>
</main>