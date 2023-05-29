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
    <Login on:close={() => bindModal = false}/> //dispatching event close from component login
  </ModalBasic>

  // When the backdrop is clicked, the modal will close by default. To disable that behavior, add the prop closeClickOutside set to false. 
  <ModalBasic bind:showModal component={Login} closeClickOutside={false} />



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
