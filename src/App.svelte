<script lang="ts">
  import { action, today, workType } from './store/store';
  import { onDestroy, onMount } from 'svelte';
  import { DefaultWorkDuration, Keys, MagicNumber, Tasks, dataJsonURL, diAudioPaths, endAudioPaths } from './config';
  import { getIntDefault, initItem } from './store/local';
  import { resolveResource } from "@tauri-apps/api/path";
  import { readTextFile } from "@tauri-apps/api/fs";
  import { convertFileSrc } from "@tauri-apps/api/tauri";
  import { addAudio, addEndAudio } from './utils';
  import { ClassContainer, TextColors } from './style';
  import Footbar from './components/footbar.svelte';
  import TimeCounter from './components/time-counter.svelte';
  import Appbar from './components/appbar.svelte';

  onMount(async () => {
    action.initData(
      getIntDefault(Keys.today(), 0),
      getIntDefault(Keys.total(Tasks.default), 0),
      getIntDefault(Keys.defaultWorkDuration, DefaultWorkDuration)
    )

    const resourcePath = await resolveResource(dataJsonURL)
    const data = JSON.parse(await readTextFile(resourcePath))
    initItem(Keys.defaultWorkDuration, data.defaultWorkDuration.toString())
    initItem(Keys.defaultBreakDuration, data.defaultBreakDuration.toString())

    for (const v of diAudioPaths) {
      // console.log("path: ", v)
      const audioPath = await resolveResource(v)
      const audio = new Audio(convertFileSrc(audioPath))
      audio.loop = true
      addAudio(v, audio)
    }

    for (const v of endAudioPaths) {
      const audioPath = await resolveResource(v)
      addEndAudio(v, new Audio(convertFileSrc(audioPath)))
    }
  })

  let mainStyle = ""
  $: {
    const index = Math.floor($today / MagicNumber)
    const arr = TextColors[$workType]??TextColors[1]
    const color = arr[index]??arr[MagicNumber]
    mainStyle = ClassContainer + color 
  }
</script>

<div class="{mainStyle}">
  <Appbar />
  <TimeCounter />
  <Footbar />
</div>