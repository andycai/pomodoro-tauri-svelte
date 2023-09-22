<script lang="ts">
  import { appWindow } from "@tauri-apps/api/window";
  import PomodoroCount from "./pomodoro-count.svelte";
  import Close from "svelte-material-icons/CloseCircle.svelte";

  //
</script>

<div class="flex flex-row justify-between pt-1 px-1 text-lg">
  <PomodoroCount />
  <div class="flex flex-row justify-end space-x-1">
    <div class="cursor-pointer" on:click={() => appWindow.close() }>
      <Close />
    </div>
  </div>
</div>