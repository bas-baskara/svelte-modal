This is a very simple modal that accept customizable svelte component

## How To Use


```javascript
<script>
  import {ModalBasic} from "svelte-modal-basic"
  import {Login} from "$lib/components"

  let showModal = false


  </script>

  ...

  <button on:click={() => showModal = true}>Log in</button> //set showModal to true will open the modal

  <ModalBasic bind:showModal component={Login} />


```


$lib/components/Login.svelte

```javascript
<script>
  import {createEventDispatcher} from 'svelte'

  const dispatch = createEventDispatcher()


  </script>

  ...

  
    <div class="mt-4 flex items-center justify-end gap-4">
      <button class="text-white bg-gray-400 hover:bg-gray-500 px-2 py-1 rounded" on:click={() => {dispatch('close')}}>Cancel</button> //dispatch with name close will close the modal. Click event outside the component Login also will close the modal.
      <button on:click={submit} class="text-gray-400 hover:bg-gray-300 hover:text-black px-2 py-1 rounded">Create</button>
    </div>


```
