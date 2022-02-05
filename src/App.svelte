<script>
// circle
	import { circleData } from "./data.js";

// tweening
	import { tweenData } from "./data.js";
	import { tweened } from "svelte/motion";
	const tweenedX = tweened(tweenData.map((d) => d.foo));
	const setFoo = function () {
		tweenedX.set(tweenData.map((d) => d.foo));
	};
	const setBar = function () {
		tweenedX.set(tweenData.map((d) => d.bar));
	};

// working


</script>

<main>
<!-- working -->
	<div class="chart">
		<svg>
			<!-- y axis -->
			<g class="axis y-axis">
				<g class="tick">
					<line x2="100%"></line>
					<text y="-4"></text>
				</g>
			</g>
			<g class="axis x-axis">
				<g class="tick">
					<line x2="100%" transform=""></line>
					<text x="" y="-4"></text>
				</g>
			</g>
			<g class="bars">
				<rect x="" y="" width="" height=""></rect>
			</g>

		</svg>
	</div>

	<hr />
<!-- cirlce -->
	<svg width="400" height="100">
	{#each circleData as d}
		<circle cx={d.x + "%"} cy="50%" r={d.r} fill="black" />
	{/each}
	</svg><hr />
	<svg width="100" height="100">
		<circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
	</svg><hr />
<!-- rectangle -->
	<svg width="400" height="180">
		<rect x="50" y="20" rx="20" ry="20" width="150" height="150"
		style="fill:red;stroke:black;stroke-width:5;opacity:0.5" />
	</svg><hr />
<!-- ellipse -->
	<svg height="140" width="500">
		<ellipse cx="200" cy="80" rx="100" ry="50"
		style="fill:yellow;stroke:purple;stroke-width:2" />
	</svg><hr />
	<svg height="150" width="500">
		<ellipse cx="240" cy="100" rx="220" ry="30" style="fill:purple" />
		<ellipse cx="220" cy="70" rx="190" ry="20" style="fill:lime" />
		<ellipse cx="210" cy="45" rx="170" ry="15" style="fill:yellow" />
	</svg><hr />
<!-- line -->
	<svg height="210" width="500">
		<line x1="0" y1="0" x2="200" y2="200" style="stroke:rgb(255,0,0);stroke-width:2" />
	</svg><hr />
<!-- polygon -->
	<svg height="250" width="500">
		<polygon points="220,10 300,210 170,250 123,234" style="fill:lime;stroke:purple;stroke-width:1" />
	</svg><hr />
	<svg height="200" width="500">
		<polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
		style="fill:none;stroke:black;stroke-width:3" />
	</svg><hr />
<!-- path -->
	<svg height="210" width="400">
		<path d="M150 0 L75 200 L225 200 Z" />
	</svg><hr />
<!-- text -->
	<svg height="60" width="200">
		<text x="0" y="15" fill="red" transform="rotate(30 20,40)">I love SVG</text>
	</svg><hr />
<!-- drawing -->
	<svg height="80" width="300">
		<g fill="none" stroke="black">
			<path stroke-width="2" d="M5 20 l215 0" />
			<path stroke="blue" stroke-width="4" d="M5 40 l215 0" />
			<path stroke-width="6" d="M5 60 l215 0" />
		</g>
	</svg><hr />
	<svg height="80" width="300">
		<g fill="none" stroke="black" stroke-width="4">
			<path stroke-dasharray="5,5" d="M5 20 l215 0" />
			<path stroke-dasharray="10,10" d="M5 40 l215 0" />
			<path stroke-dasharray="20,10,5,5,5,10" d="M5 60 l215 0" />
		</g>
	</svg><hr />
<!-- tweening -->
	<button on:click={setFoo}>Foo</button>
	<button on:click={setBar}>Bar</button>
	<p> Your values:
		{#each $tweenedX as x}
			{x}
		{/each}
	</p>

</main>

<style>
/* working */
	.chart {
			width: 100%;
			max-width: 500px;
			margin: 0 auto;
		}
		svg {
			position: relative;
			width: 100%;
			height: 200px;
		}
		.tick {
			font-family: Helvetica, Arial;
			font-size: .725em;
			font-weight: 200;
		}


		
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>