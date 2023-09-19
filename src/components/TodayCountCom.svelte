<script lang="ts">
  import ClockOutline from "svelte-material-icons/ClockOutline.svelte";
  import CoffeeOutline from "svelte-material-icons/CoffeeOutline.svelte";
  import { IconSize, WorkType } from '../config';
  import { today, total, workType } from "../store/store";
  import { changeAudio, playAudio } from "../utils";

  console.log("render today count")

  function change() {
    playAudio(changeAudio())
  }

</script>

<div class="flex flex-row flex-none ml-1">
  <div on:click={change}>
{#if $workType === WorkType.Work}
  <ClockOutline class="cursor-pointer" size="{IconSize}" />
{:else}
  <CoffeeOutline class="cursor-pointer" size="{IconSize}" />
{/if}
  </div>
  <span class="text-xs pt-2">{ $total }/{ $today }</span>
</div>