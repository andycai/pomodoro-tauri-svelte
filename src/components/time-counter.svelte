<script lang="ts">
  import { count } from "../store/store";
  import { convertMinuteString, convertSecondString } from "../utils";

  // console.log("render TimeCounter", $count);

</script>

<div class="flex flex-col items-center font-black" data-tauri-drag-region>
  <h1 class="text-7xl" data-tauri-drag-region>{ convertMinuteString($count) }</h1>
  <h4 class="text-7xl" data-tauri-drag-region>{ convertSecondString($count) }</h4>
</div>