<script lang="ts">
	import ModalBasic from '$lib/ModalBasic.svelte';

	let showModal = false;
	$: console.log('showmodal', showModal);
</script>

<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<button on:click={() => (showModal = true)}>showModal</button>

<ModalBasic {showModal} component={null} on:close={() => (showModal = false)} />
