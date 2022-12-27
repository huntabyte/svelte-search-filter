<script lang="ts">
	import { createSearchStore, searchHandler } from '$lib/stores/search';
	import type { PageData } from './$types';

	export let data: PageData;

	const searchProducts = data.products.map((product: any) => ({
		...product,
		searchTerms: `${product.title} ${product.description} ${product.category} ${product.brand}`
	}));

	const searchStore = createSearchStore(searchProducts);

	searchStore.subscribe((model) => searchHandler(model));
</script>

<div class="container">
	<h1>Search/Filter</h1>
	<input type="search" placeholder="Search..." bind:value={$searchStore.search} />
</div>
<div class="product-grid">
	{#each $searchStore.filtered as product}
		<div class="product">
			<h2>{product.title}</h2>
			<p>{product.description}</p>
			<p class="badge">{product.category}</p>
			<p>{product.brand}</p>
		</div>
	{/each}
</div>

<style>
	.container {
		margin-inline: auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-top: 1.5rem;
	}

	.product {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: flex-start;
		margin: 1rem;
		padding: 1rem;
		border: 1px solid #ccc;
		border-radius: 0.5rem;
		gap: 0.5rem;
	}

	.product-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
		grid-gap: 1rem;
	}

	.badge {
		display: inline-block;
		padding: 0.25em 0.4em;
		font-size: 75%;
		font-weight: 700;
		line-height: 1;
		text-align: center;
		white-space: nowrap;
		vertical-align: baseline;
		border-radius: 0.25rem;
		background-color: var(--color-primary-500);
		color: var(--color-gray-1000);
	}
</style>
