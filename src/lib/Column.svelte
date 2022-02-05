<script lang="ts">
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';

	export let name;
	export let items;
	export let onDrop;

	const flipDurationMs = 300;

	function handleDndConsiderCards(e) {
		items = e.detail.items;
	}

	function handleDndFinalizeCards(e) {
		onDrop(e.detail.items);
	}
</script>

<section class="wrapper">
	<header class="column-title">
		<h2>{name}</h2>
	</header>
	<div
		class="column-content"
		use:dndzone={{ items, flipDurationMs, zoneTabIndex: -1 }}
		on:consider={handleDndConsiderCards}
		on:finalize={handleDndFinalizeCards}
	>
		{#each items as card (card.id)}
			<article class="card" animate:flip={{ duration: flipDurationMs }}>
				{card.name}
			</article>
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
		height: 4em;
		width: 100%;
		margin: 0.4em 0;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #dddddd;
		border: 1px solid #333333;
	}
</style>
