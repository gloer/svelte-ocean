<script>
	import { onMount } from "svelte";
	import Chart from "chart.js";
	
	async function renderChart() {

		const res = await fetch("https://pomber.github.io/covid19/timeseries.json");
		const json = await res.json();
		const norgeData = json["Norway"]

		// Starter med første registrerte smitte
		const norge = norgeData.filter(land => land.confirmed > 0)
		

		const dates = norge.map(land => land.date)
		const confirmed = norge.map(land => land.confirmed)
		const deaths = norge.map(land => land.deaths)

		console.log(norge);


		var ctx = document.getElementById("myChart").getContext("2d");
		var chart = new Chart(ctx, {
		type: "line",
		data: {
			labels: dates,
			datasets: [
			{
				label: "Smittede",
				backgroundColor: "rgb(255, 99, 132)",
				borderColor: "rgb(120, 99, 132)",
				data: confirmed
			},
			{
				label: "Døde",
				backgroundColor: "orange)",
				borderColor: "rgb(120, 99, 132)",
				data: deaths
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