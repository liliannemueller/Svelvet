<script lang="ts">
	import { Svelvet, Minimap, Node } from '$lib';
	import CustomEdge from '../../example-components/CustomEdge.svelte';
</script>

<body>
	<div class="wrapper">
		<Svelvet theme="dark" width={800} height={500} controls>
			<Node id="node1" label="test" resizable />
			<Node
				on:connection={() => console.log('node2 connected')}
				on:disconnection={() => console.log('node2 disconnected')}
				position={{ x: 300, y: 300 }}
				dimensions={{ width: 400, height: 100 }}
				id="node2"
				label="test"
				edge={CustomEdge}
			/>
			<Node label="what" position={{ x: 10, y: 200 }} inputs={3} TD />
			<Minimap slot="minimap" />
		</Svelvet>
	</div>
</body>

<style>
	.wrapper {
		display: flex;
		border: solid 1px black;
		border-radius: 20px;
		overflow: hidden;
		box-shadow: 0 0 40px 0 rgba(37, 37, 37, 0.5);
	}
	body {
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: gray;
		width: 100vw;
		height: 100vh;
		padding: 0;
		margin: 0;
	}
	/* :root[theme='dark'] {
		--node-selection-color: blue;
		--node-color: red;
		--background-color: green;
	}
	:root[theme='light'] {
		--node-selection-color: red;
		--node-color: blue;
		--background-color: yellow;
	} */

	:root[svelvet-theme='my-other-theme'] {
		--node-color: hsl(225, 30%, 50%);
		--node-border-color: hsl(225, 20%, 40%);
		--node-selection-color: hsl(45, 90%, 60%);
		--text-color: hsl(0, 0%, 100%);
		--node-shadow: var(--shadow-elevation-medium);

		--background-color: hsl(225, 20%, 27%);
		--dot-color: hsl(225, 10%, 50%);

		--accent-color: hsl(45, 90%, 60%);
		--primary-color: hsl(225, 30%, 66%);

		--edge-color: hsl(0, 0%, 100%);
		--target-edge-color: hsl(225, 20%, 40%);
		--edge-shadow: var(--shadow-elevation-medium);

		--anchor-color: hsl(45, 90%, 67%);
		--anchor-border-color: hsl(45, 90%, 87%);
		--anchor-connected: hsl(45, 90%, 100%);
		--anchor-connected-border: hsl(225, 20%, 20%);

		--anchor-connecting: hsl(225, 30%, 40%);
		--anchor-connecting-border: hsl(0, 0%, 100%);

		--anchor-hovering: hsl(225, 20%, 46%);
		--anchor-hovering-border: hsl(0, 0%, 0%);

		--minimap-background-color: hsl(225, 20%, 27%);

		--minimap-node-color: hsl(225, 30%, 20%);

		--controls-background-color: hsl(225, 20%, 27%);
		--controls-text-color: hsl(0, 0%, 100%);

		--theme-toggle-text-color: hsl(0, 0%, 100%);
		--theme-toggle-color: hsl(225, 20%, 27%);
	}
</style>
