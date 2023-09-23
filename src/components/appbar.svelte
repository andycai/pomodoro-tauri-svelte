<script lang="ts">
  import { appWindow } from "@tauri-apps/api/window";
  import PomodoroCount from "./pomodoro-count.svelte";
  import Close from "svelte-material-icons/CloseCircle.svelte";

  //
</script>

<div class="flex flex-row justify-between pt-1 px-1">
  <PomodoroCount />
  <button title="Close Window" class="flex flex-row justify-end space-x-1" on:click={() => appWindow.close() }>
    <Close class="w-4 h-4" />
  </button>
</div>