<script lang="ts">
	import { flip } from 'svelte/animate';
	import { fade } from 'svelte/transition';
	import { cubicIn } from 'svelte/easing';
	import { dndzone, SHADOW_ITEM_MARKER_PROPERTY_NAME } from 'svelte-dnd-action';

	export let column;
	export let onDrop;

	const flipDurationMs = 300;

	function handleDndConsiderCards(e) {
		column.items = e.detail.items;
	}

	function handleDndFinalizeCards(e) {
		onDrop(e.detail.items);
	}
</script>

<section class="wrapper">
	<header class="column-title">
		<h2>{column.name}</h2>
	</header>
	<div
		class="column-content"
		use:dndzone={{ items: column.items, flipDurationMs, zoneTabIndex: -1 }}
		on:consider={handleDndConsiderCards}
		on:finalize={handleDndFinalizeCards}
	>
		{#each column.items as card (card.id)}
			<div animate:flip={{ duration: flipDurationMs }}>
				<article class="card">
					{card.name}
					{#if card[SHADOW_ITEM_MARKER_PROPERTY_NAME]}
						<div in:fade={{ duration: 200, easing: cubicIn }} class="custom-shadow-item">
						</div>
					{/if}
				</article>
			</div>
		{/each}
	</div>
</section>

<style>
	.wrapper {
		height: 100%;
		width: 100%;
		overflow-y: hidden;
	}
	.column-title {
		height: 2.5em;
		font-weight: bold;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.column-content {
		height: calc(100% - 2.5em);
		overflow-y: scroll;
	}
	.card {
		position: relative;
		height: 4em;
		width: 100%;
		margin: 0.4em 0;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #dddddd;
		border: 1px solid #333333;
	}

	.custom-shadow-item {
		position: absolute;
		top: 0; left:0; right: 0; bottom: 0;
		visibility: visible;
		border: 1px dashed grey;
		background: rgba(0, 0, 0, 0.5);
		opacity: 0.5;
		margin: 0;
	}
</style>
