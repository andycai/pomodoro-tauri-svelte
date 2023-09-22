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

<button on:click={change}>
{#if $workType === WorkType.Work}
  <ClockOutline />
{:else}
  <CoffeeOutline />
{/if}
</button>
<span class="text-xs ml-1 pt-0">{ $total }/{ $today }</span>