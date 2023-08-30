This is a very simple modal that accept customizable svelte component

## How To Use

```javascript
<script>
  import {ModalBasic} from "svelte-modal-basic"
  import {Login} from "$lib/components"

  let showModal = false


  </script>

  ...

  <button on:click={() => showModal = true}>Log in</button> //Setting showModal to true will open the modal

  <ModalBasic bind:showModal component={Login} />
  // or
  <ModalBasic bind:showModal>
    <Login on:close={() => bindModal = false} // dispatching event close from component login
    />
  </ModalBasic>

/*
  The following code uses the ModalBasic component to display a modal dialog.
  By default, clicking outside the modal's backdrop will close the modal.
  To prevent this behavior, set the prop "closeClickOutside" to false.

  Additionally, you can listen for the "close" event on the parent component
  and handle it to close the modal. In this example, the "showModal" variable
  is used to control the visibility of the modal.
*/

<ModalBasic
  {showModal}          // A boolean variable controlling the modal's visibility
  component={Login}    // The content component to be displayed inside the modal
  closeClickOutside={false} // Prevent closing the modal by clicking outside
  on:close={() => showModal = false} // Listen for the "close" event to hide the modal
/>


```

$lib/components/Login.svelte

```javascript
<script>
  import {createEventDispatcher} from 'svelte'

  const dispatch = createEventDispatcher()


  </script>

  ...


    <div class="mt-4 flex items-center justify-end gap-4">
      <button class="text-white bg-gray-400 hover:bg-gray-500 px-2 py-1 rounded" on:click={() => {dispatch('close')}}>Cancel</button> //Dispatching an event with the name 'close' will close the modal. Clicking outside the Login component will also close the modal if the children are passed as **props**, not through the **slot**.
      <button on:click={submit} class="text-gray-400 hover:bg-gray-300 hover:text-black px-2 py-1 rounded">Create</button>
    </div>


```
