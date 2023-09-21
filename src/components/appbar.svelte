<script lang="ts">
  import { appWindow } from "@tauri-apps/api/window";
  import PomodoroCount from "./pomodoro-count.svelte";
  import RefreshButton from "./refresh-button.svelte";
  import Close from "svelte-material-icons/CloseCircle.svelte";

  //
</script>

<div class="flex flex-row justify-between">
  <div class="ml-1 mt-1">
    <PomodoroCount />
  </div>
  <div class="flex flex-row justify-end mt-1 space-x-1 mr-1">
    <RefreshButton />
    <div class="cursor-pointer" on:click={() => appWindow.close() }>
      <Close size={14} />
    </div>
  </div>
</div>