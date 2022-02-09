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
import { scaleLinear } from 'd3-scale';
import { gridData } from "./data.js";

const padding = {top:20,right:40,bottom:40,left:25};
let width = 150, height = 150;
const xxTicks = [0, 4, 8, 12, 16, 20];
const yyTicks = [0, 2, 4, 6, 8, 10, 12];
$: xScale = scaleLinear().domain([0,20]).range([padding.left, width-padding.right]);
$: yScale = scaleLinear().domain([0,12]).range([height-padding.bottom, padding.top]);
</script>

<main>
<!-- working -->
<svg width='150' height='150' style='background-color:red' preserveAspectRatio='none'>
	<g fill="blue">
		<rect x="10" y="10" height="100" width="100" transform="translate(0,0)"
		style="stroke:green; fill:yellow"/>
	</g>
</svg>
<svg width={width} height={height} style='background-color:yellow'>

	<g class="x-axis">
		{#each xxTicks as tick}
		<g transform="translate(0, {yScale(tick)})">
			<line x1="{padding.left}" x2="{xScale(22)}" stroke="black" />
		</g>
		{/each}
	</g>
	<g class="y-axis">
		{#each xxTicks as tick}
		<g transform="translate({xScale(tick)},0)">
			<line y1="{yScale(0)}" y2="{yScale(13)}" stroke="black" />
		</g>
		{/each}
	</g>
	{#each gridData as point}
		<circle cx='{xScale(point.x)}' cy='{yScale(point.y)}' r='5'/>
	{/each}


</svg>
<hr />
<!-- gray boxes -->
	<svg width="800" height="200">
		<g transform="translate(70, 20)">
			<rect width="15" height="15" x="0" y="0"></rect>
			<rect width="15" height="15" x="0" y="20"></rect>
			<rect width="15" height="15" x="0" y="40"></rect>
			<rect width="15" height="15" x="0" y="60"></rect>
			<rect width="15" height="15" x="20" y="0"></rect>
			<rect width="15" height="15" x="20" y="20"></rect>
			<rect width="15" height="15" x="20" y="40"></rect>
			<rect width="15" height="15" x="20" y="60"></rect>
		</g>
	</svg><hr />
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
<!-- marker -->
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
	<defs>
		<!-- arrowhead marker definition -->
		<marker id="arrow" viewBox="0 0 10 10" refX="5" refY="5"
		markerWidth="6" markerHeight="6"
		orient="auto-start-reverse">
			<path d="M 0 0 L 10 5 L 0 10 z" />
		</marker>
		<!-- simple dot marker definition -->
		<marker id="dot" viewBox="0 0 10 10" refX="5" refY="5"
		markerWidth="5" markerHeight="5">
			<circle cx="5" cy="5" r="5" fill="red" />
		</marker>
	</defs>
	<!-- Coordinate axes with a arrowhead in both direction -->
	<polyline points="10,10 10,90 90,90" fill="none" stroke="black"
	marker-start="url(#arrow)" marker-end="url(#arrow)" />
	<!-- Data line with polymarkers -->
	<polyline points="15,80 29,50 43,60 57,30 71,40 85,15" fill="none" stroke="grey"
	marker-start="url(#dot)" marker-mid="url(#dot)"  marker-end="url(#dot)" />
</svg><hr>
<!-- mask -->
	<svg viewBox="-10 -10 120 120">
		<mask id="myMask">
			<!-- Everything under a white pixel will be visible -->
			<rect x="0" y="0" width="100" height="100" fill="white" />
			<!-- Everything under a black pixel will be invisible -->
			<path d="M10,35 A20,20,0,0,1,50,35 A20,20,0,0,1,90,35 Q90,65,50,95 Q10,65,10,35 Z" fill="black" />
		</mask>
		<polygon points="-10,110 110,110 110,-10" fill="orange" />
		<!-- with this mask applied, we "punch" a heart shape hole into the circle -->
		<circle cx="50" cy="50" r="50" mask="url(#myMask)" />
	</svg><hr>
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
	rect {
		fill: #ddd;
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>