<script lang="ts">
	import { fade } from "svelte/transition";
	import { onMount, onDestroy } from "svelte";
  import cx from "classnames";
	import ClickOutside from 'click-outside-element'

	export let showModal = false;
	export let component: any;

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

	onMount(() => {
		theModal = document.getElementById("modal");
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
  <div class={cx(component ? "":"bg-white p-2")} use:ClickOutside={() => showModal = false}>
    {#if component}
      <svelte:component this={component} />
    {:else}
      <div>empty</div>
    {/if}
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
	.px-2 {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
	}
	.mx-auto {
    margin-left: auto;
    margin-right: auto;
	}
	.py-3 {
    padding-top: 0.75rem;
    padding-bottom: 0.75rem;
	}
	.px-2 {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
	}
	.bg-white {
    --tw-bg-opacity: 1;
    background-color: rgb(255 255 255 / var(--tw-bg-opacity));
	}
	.rounded-lg {
    border-radius: 0.5rem;
	}
	.text-xl {
    font-size: 1.25rem;
    line-height: 1.75rem;
	}
	.mt-4 {
    margin-top: 1rem;
	}
	.gap-4 {
    gap: 1rem;
	}
	.justify-end {
    justify-content: flex-end;
	}
	.items-center {
    align-items: center;
	}
	.flex {
    display: flex;
	}
	.mt-4 {
    margin-top: 1rem;
	}
	.p-2 {
    padding: 0.5rem;
	}
	.bg-gray-200 {
    --tw-bg-opacity: 1;
    background-color: rgb(229 231 235 / var(--tw-bg-opacity));
	}
	.border-b {
    border-bottom-width: 1px;
	}
	.border-y-0 {
    border-top-width: 0px;
    border-bottom-width: 0px;
	}
	.border-x-0 {
    border-left-width: 0px;
    border-right-width: 0px;
	}
	.rounded-t {
    border-top-left-radius: 0.25rem;
    border-top-right-radius: 0.25rem;
	}
	.w-full {
    width: 100%;
	}
	.gap-4 {
    gap: 1rem;
	}
	.justify-end {
    justify-content: flex-end;
	}
	.items-center {
    align-items: center;
	}
	.flex {
    display: flex;
	}
	.mt-4 {
    margin-top: 1rem;
	}
	.text-white {
    --tw-text-opacity: 1;
    color: rgb(255 255 255 / var(--tw-text-opacity));
	}
	.py-1 {
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
	}
	.px-2 {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
	}
	.bg-gray-400 {
    --tw-bg-opacity: 1;
    background-color: rgb(156 163 175 / var(--tw-bg-opacity));
	}
	.rounded {
    border-radius: 0.25rem;
	}
	.text-gray-400 {
    --tw-text-opacity: 1;
    color: rgb(156 163 175 / var(--tw-text-opacity));
	}
	.py-1 {
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
	}
	.px-2 {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
	}
	.rounded {
    border-radius: 0.25rem;
	}

	@media (min-width: 640px) {
		.sm\:px-0 {
			padding-left: 0px;
			padding-right: 0px;
		}
		.sm\:max-w-\[90\%\] {
			max-width: 90%;
		}
		.sm\:px-4 {
			padding-left: 1rem;
			padding-right: 1rem;
		}
	}

	@media (min-width: 768px) {
		.md\:w-\[40rem\] {
			width: 40rem;
		}		
	}


	@media (min-width: 1024px) {
		.lg\:px-6 {
			padding-left: 1.5rem;
			padding-right: 1.5rem;
		}
	}




</style>