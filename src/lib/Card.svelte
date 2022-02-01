<script lang="ts">
	export let card: { id: number; title: string; description: string };
</script>

<article class="border round">
	<header>
		<h3>{card.title}</h3>
	</header>
	<div class="description">{card.description ?? ''}</div>
</article>

<style>
	header {
		padding: 0 0.5rem;
		border-bottom: 1px solid #eee;
	}
	.description {
		padding: 0.5rem;
	}
</style>
