<script lang="ts">
  import RefreshCircle from "svelte-material-icons/RefreshCircle.svelte";
  import { IconSize, Status, WorkType } from "../config";
  import { action, status, workType } from "../store/store";

  console.log("render refresh")
</script>

<div on:click={action.reset}>
{#if $status === Status.Pause || $workType === WorkType.Break}
  <RefreshCircle class="cursor-pointer" size={14} />
{/if}
</div>