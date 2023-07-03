<script>
	import CarsInfo from './CarsInfo.svelte';
	
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	  <CarsInfo/>
</section>

<style lang="postcss">
	:global(html) {
	  background-color: theme(colors.gray.100);
	}
  </style>