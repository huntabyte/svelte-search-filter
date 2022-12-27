<script lang="ts">
	import type { PageData } from './$types';

	export let data: PageData;
</script>

<div class="container">
	<h1>Search/Filter</h1>
	<input type="search" placeholder="Search..." />
</div>
<pre>{JSON.stringify(data.products, null, 2)}</pre>

<style>
	.container {
		margin-inline: auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding-top: 1.5rem;
	}
</style>
