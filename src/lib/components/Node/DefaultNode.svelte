<script context="module" lang="ts">
	import Resizer from '$lib/components/Resizer/Resizer.svelte';
	import Anchor from '$lib/components/Anchor/Anchor.svelte';
	import { get } from 'svelte/store';
	import { getContext } from 'svelte';
	import type { Node } from '$lib/types';
</script>

<script lang="ts">
	const dynamic = getContext<boolean>('dynamic');
	const node = getContext<Node>('node');

	// Props
	export let selected: boolean;

	// External stores
	const label = node.label;
	const borderRadius = node.borderRadius;
	const textColor = node.textColor;
	const inputs = node.inputs;
	const outputs = node.outputs;
	const resizable = node.resizable;
	const directionStore = node.direction;

	//Subscriptions
	$: direction = $directionStore;

	let top = get(node.direction) === 'TD' ? true : false;
	let bottom = get(node.direction) === 'TD' ? true : false;

	let left = get(node.direction) === 'TD' ? false : true;
	let right = get(node.direction) === 'TD' ? false : true;
</script>

<div class:selected class="default-node" style:border-radius="{$borderRadius}px">
	{#if dynamic}
		{#each { length: $inputs } as _, i}
			<Anchor on:connection on:disconnection />
		{/each}
		{#each { length: $outputs } as _, i}
			<Anchor on:connection on:disconnection />
		{/each}
	{:else}
		<div class="input-anchors" class:top class:left>
			{#each { length: $inputs } as _, i (i)}
				<Anchor on:connection on:disconnection input direction={top ? 'north' : 'west'} />
			{/each}
		</div>
		<div class="output-anchors" class:bottom class:right>
			{#each { length: $outputs } as _, i (i)}
				<Anchor on:connection on:disconnection output direction={top ? 'south' : 'east'} />
			{/each}
		</div>
	{/if}
	<p style:color={$textColor}>{$label}</p>

	{#if $resizable}
		<Resizer width height rotation />
	{/if}
</div>

<style>
	.default-node {
		display: flex;
		justify-content: center;
		align-items: center;
		position: relative;
		box-sizing: border-box;
		width: inherit;
		height: inherit;
	}
	p {
		font-size: 20px;
		line-height: 20px;
		text-align: center;
		user-select: none;
	}
	.input-anchors,
	.output-anchors {
		display: flex;
		position: absolute;
		justify-content: center;
		align-items: center;
		z-index: 1;
		pointer-events: none;
		/* outline: solid 1px red; */
	}

	.top,
	.bottom {
		width: 100%;
		justify-content: space-around;
	}

	.top {
		transform: translate(0px, -50%);
		top: 0px;
	}

	.bottom {
		transform: translate(0px, 50%);
		bottom: 0px;
	}

	.left,
	.right {
		height: 100%;
		flex-direction: column;
		justify-content: space-around;
	}

	.left {
		transform: translate(-50%);
		left: 0px;
	}

	.right {
		transform: translate(50%);
		right: 0px;
	}
</style>
