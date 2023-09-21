<script lang="ts">
  import ClockOutline from "svelte-material-icons/ClockOutline.svelte";
  import CoffeeOutline from "svelte-material-icons/CoffeeOutline.svelte";
  import { WorkType } from '../config';
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
  <ClockOutline class="cursor-pointer" size="{15}" />
{:else}
  <CoffeeOutline class="cursor-pointer" size="{15}" />
{/if}
  </div>
  <span class="text-xs ml-1 pt-0">{ $total }/{ $today }</span>
</div>