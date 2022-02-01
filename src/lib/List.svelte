<script lang="ts">
	import Card from './Card.svelte';
	export let list: {
		id: number;
		title: string;
		cards: { id: number; title: string; description: string }[];
	};
</script>

<section class="list border round">
	<header class="list-header">
		<h2>{list.title}</h2>
	</header>
	<div class="list-items">
		{#each list.cards as card (card.id)}
			<Card {card} />
		{/each}
	</div>
</section>

<style>
	.list {
		width: 272px;
	}
	.list-items {
		padding: 0.5em;
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.list-header {
		padding: 0 0.5rem;
		border-bottom: 1px solid #eee;
	}
</style>
