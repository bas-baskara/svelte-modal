<script lang="ts">
	import { fade } from 'svelte/transition';
	import { onMount, onDestroy } from 'svelte';
	import ClickOutside from 'click-outside-element';

	export let showModal = false;
	export let component: any | undefined = undefined;
	export let closeClickOutside = true;

	let theModal: HTMLElement | null, theModalParent: HTMLElement | null;

	const moveModalToBody = () => {
		if (theModal) {
			document.body.appendChild(theModal);
			document.body.classList.add('overflow-hidden');
		}
	};

	const moveModalBack = () => {
		if (theModal && theModalParent) {
			theModalParent.appendChild(theModal);
			document.body.classList.remove('overflow-hidden');
		}
	};

	const clickOutSide = () => {
		if (closeClickOutside) {
			showModal = false;
		}
	};

	onMount(() => {
		theModal = document.getElementById('modal');
		if (theModal) {
			theModalParent = theModal.parentElement;
		}
	});

	onDestroy(() => {
		moveModalBack();
	});

	$: if (showModal) {
		moveModalToBody();
	} else {
		moveModalBack();
	}
</script>

{#if showModal}
	<div
		id="modal"
		class="fixed z-[100] bg-gray-500/75 inset-0 w-screen h-screen overflow-hidden grid place-content-center"
		transition:fade
	>
		<div use:ClickOutside={clickOutSide}>
			<slot>
				{#if component}
					<svelte:component this={component} on:close={() => (showModal = false)} />
				{:else}
					<div class="bg-white p-2">empty</div>
				{/if}
			</slot>
		</div>
	</div>
{/if}

<style scoped>
	.bg-gray-500\/75 {
		background-color: rgb(107 114 128 / 0.75);
	}
	.overflow-hidden {
		overflow: hidden;
	}
	.place-content-center {
		place-content: center;
	}
	.w-screen {
		width: 100vw;
	}
	.h-screen {
		height: 100vh;
	}
	.grid {
		display: grid;
	}
	.z-\[100\] {
		z-index: 100;
	}
	.inset-0 {
		top: 0px;
		right: 0px;
		bottom: 0px;
		left: 0px;
	}
	.fixed {
		position: fixed;
	}
	.bg-white {
		--tw-bg-opacity: 1;
		background-color: rgb(255 255 255 / var(--tw-bg-opacity));
	}
	.p-2 {
		padding: 0.5rem;
	}
</style>
