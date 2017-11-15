<template>
	<div class="hello">
		<h1>Vue Callback abcjs Demo</h1>
		<p>This is a simple app that shows the callback from abcjs.</p>
		<p class="instructions">Click around on the various parts of the sheet music and see what the resultant output is.</p>
		<p>The only addition to the standard vue-cli app's dependencies is:</p>
		<pre>npm install abcjs --save</pre>
		<p>The only necessary code to make this work is:</p>
		<pre>import abcjs from "abcjs";

const engraverParams = {
  listener: {
    highlight: this.highlight,
  }
};
abcjs.renderAbc("paper", this.tune, {},
  engraverParams, {});</pre>
		<div class="output">
			Output
			<div class="tune-number">Tune Number: <i>{{tuneNumber}}</i></div>
			<div class="abcelem">Struct returned from callback:<br><i>{{elem}}</i></div>
		</div>
		<p class="instructions">Click around on the various parts of the sheet music and see what the resultant output is.</p>
		<div id="paper"></div>
	</div>
</template>

<script>
	import abcjs from "abcjs";

	export default {
		mounted: function () {
			const engraverParams = {
				listener: {
					highlight: this.highlight,
				}
			};
			abcjs.renderAbc("paper", this.tune, {}, engraverParams, {});
		},
		name: 'hello',
		data () {
			return {
				elem: {},
				tuneNumber: "",
				tune: `X:1
T: Cooley's
M: 4/4
L: 1/8
R: reel
K: Emin
D2|:"Em"EB{c}BA B2 EB|~B2 AB dBAG|"D"FDAD BDAD|FDAD dAFD|
"Em"EBBA B2 EB|B2 AB defg|"D"afe^c dBAF|1"Em"DEFD E2 D2:|2"Em"DEFD E2 gf||
|:"Em"eB B2 efge|eB B2 gedB|"D"A2 FA DAFA|A2 FA defg|
"Em"eB B2 eBgB|eB B2 defg|"D"afe^c dBAF|1"Em"DEFD E2 gf:|2"Em"DEFD E4|]
`
			}
		},
		methods: {
			highlight(abcElem, tuneNumber) {
				// remove the abselem member because it is circular.
				const elem = Object.assign({}, abcElem);
				delete elem.abselem;
				this.elem = elem;
				this.tuneNumber = tuneNumber;
			},
		}
	}
</script>

<style>
	.hello {
		text-align: left;
	}
	#abc-source {
		width: 350px;
		height: 300px;
	}

	pre, .output {
		border: 1px solid #888888;
		padding: 6px;
		border-radius: 4px;
		width: 350px;
	}

	.output {
		background-color: #fbfbdc;
	}

	.output i {
		font-style: normal;
		font-weight: bold;
	}

	.instructions {
		font-weight: bold;
		color: #ff2850;
	}

</style>
