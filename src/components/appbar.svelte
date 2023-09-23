<script lang="ts">
  import { appWindow } from "@tauri-apps/api/window";
  import PomodoroCount from "./pomodoro-count.svelte";
  import Close from "../icons/close.svelte";

</script>

<div class="flex flex-row justify-between pt-1 px-1">
  <PomodoroCount />
  <button title="Close Window" class="flex flex-row justify-end space-x-1" on:click={() => appWindow.close() }>
    <Close />
  </button>
</div>