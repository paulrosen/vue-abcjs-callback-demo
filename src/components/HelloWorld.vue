<template>
	<div class="hello">
		<h1>Vue Callback abcjs Demo</h1>
		<p>This is a simple app that shows the callback from abcjs.</p>
		<p class="instructions">Click around on the various parts of the sheet music and see what the resultant output is.</p>
		<p>The only addition to the standard vue-cli app's dependencies is:</p>
		<pre>npm install abcjs --save</pre>
		<p>The only necessary code to make this work is:</p>
		<pre>import abcjs from "abcjs";

abcjs.renderAbc("paper", this.tune, {
    add_classes: true,
    clickListener: this.listener
});</pre>
		<pre>&lt;div id="paper"&gt;</pre>
		<div class="output">
			Output
			<div class="tune-number">Tune Number: <i>{{tuneNumber}}</i></div>
			<div class="classes">Classes: <i>{{classes}}</i></div>
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
			abcjs.renderAbc("paper", this.tune, { add_classes: true, clickListener: this.listener });
		},
		name: 'hello',
		data () {
			return {
				elem: {},
				tuneNumber: "",
				classes: [],
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
			listener(abcElem, tuneNumber, classes) {
				// remove the abselem member because it is circular.
				const elem = Object.assign({}, abcElem);
				delete elem.abselem;
				this.elem = elem;
				this.tuneNumber = tuneNumber;
				this.classes = classes
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
