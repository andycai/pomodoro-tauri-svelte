<script lang="ts">
  import { action } from "../store/store";
  import OperationButton from "./operation-button.svelte";
  import RefreshButton from "./refresh-button.svelte";
  import Palette from "svelte-material-icons/PaletteOutline.svelte";

  function changeTheme() {
    action.changeTheme()
  }
</script>

<div class="flex flex-row items-end mt-1 px-1">
  <button class="flex flex-row justify-start text-sm basis-1/4" title="Change Theme" on:click={changeTheme}>
    <Palette class="w-4 h-4" />
  </button>
  <OperationButton />
  <RefreshButton />
</div>