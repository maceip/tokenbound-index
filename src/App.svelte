<script lang="ts">
	import Conquest from './pages/Conquest.svelte';
	import Home from './pages/Home.svelte';
	import MyNfts from './pages/MyNFTS.svelte';
	import Bleeps from './pages/Bleeps.svelte';

	function getPage() {
		const page = document.location.hash;
		if (page === '' || page === '#') {
			console.log(`HOME`);
			document.location.assign(document.location.toString().split('#')[0] + '#home');
		}
		return page;
	}
	let page = getPage();
	window.onpopstate = function () {
		page = getPage();
	};
</script>

<MyNfts />
