<script lang="ts">
  import { appWindow } from "@tauri-apps/api/window";
  import PomodoroCount from "./pomodoro-count.svelte";
  import Close from "svelte-material-icons/CloseCircle.svelte";

  //
</script>

<div class="flex flex-row justify-between pt-1 px-1 text-lg">
  <PomodoroCount />
  <button class="flex flex-row justify-end space-x-1" on:click={() => appWindow.close() }>
    <Close />
  </button>
</div>