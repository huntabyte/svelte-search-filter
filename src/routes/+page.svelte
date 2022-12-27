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
