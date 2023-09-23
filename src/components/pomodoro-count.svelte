<script lang="ts">
  import VolumeMute from "svelte-material-icons/VolumeMute.svelte";
  import VolumeHigh from "svelte-material-icons/VolumeHigh.svelte";
  import { today, total, status } from "../store/store";
  import { changeAudio, playAudio } from "../utils";
  import { Status } from "../config";

  console.log("render today count")

  let musicOff = false 

  function change() {
    if ($status === Status.Tick) {
      musicOff = !changeAudio()
      playAudio(!musicOff)
    }
  }

</script>

<button title="Change Audio or Mute" on:click={change}>
{#if musicOff }
  <VolumeMute />
{:else}
  <VolumeHigh />
{/if}
</button>
<span class="text-xs pt-0">{ $total }/{ $today }</span>