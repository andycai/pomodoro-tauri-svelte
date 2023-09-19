<script lang="ts">
  import OperactionCom from './components/OperactionCom.svelte'
  import RefreshCom from './components/RefreshCom.svelte'
  import TimeCounterCom from './components/TimeCounterCom.svelte'
  import TodayCountCom from './components/TodayCountCom.svelte'
  import Close from "svelte-material-icons/Close.svelte";
  import { appWindow } from '@tauri-apps/api/window'
  import { action, today, workType } from './store/store';
  import { onDestroy, onMount } from 'svelte';
  import { DefaultWorkDuration, Keys, MagicNumber, Tasks, dataJsonURL, diAudioPaths, endAudioPaths } from './config';
  import { getIntDefault, initItem } from './store/local';
  import { resolveResource } from "@tauri-apps/api/path";
  import { readTextFile } from "@tauri-apps/api/fs";
  import { convertFileSrc } from "@tauri-apps/api/tauri";
  import { addAudio, addEndAudio } from './utils';
  import { ClassContainer, TextColors } from './style';

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

    for (let v of diAudioPaths) {
      // console.log("path: ", v)
      const audioPath = await resolveResource(v)
      const audio = new Audio(convertFileSrc(audioPath))
      audio.loop = true
      addAudio(v, audio)
    }

    for (let v of endAudioPaths) {
      const audioPath = await resolveResource(v)
      addEndAudio(v, new Audio(convertFileSrc(audioPath)))
    }
  })

  const getMainStyle = () => {
    const index = Math.floor($today / MagicNumber)
    const arr = TextColors[$workType]??TextColors[1]
    const color = arr[index]??arr[MagicNumber]
    return ClassContainer + color 
  }

  let mainStyle = getMainStyle()
  const unsubscribe = today.subscribe((newValue) => {
    mainStyle = getMainStyle()
  })
  const unsubscribe2 = workType.subscribe((newValue) => {
    mainStyle = getMainStyle()
  })

  onDestroy(() => {
    unsubscribe()
    unsubscribe2()
  })

</script>

<div class="{mainStyle}">
  <div class="cursor-pointer absolute right-0" on:click={() => appWindow.close() }>
    <Close size={14} />
  </div>
  <div class="flex flex-col">
    <TimeCounterCom />
    <div class="flex flex-row justify-center mt-1">
      <TodayCountCom />
      <div class="flex flex-row flex-1 grow justify-end space-x-1 mr-1">
        <RefreshCom />
        <OperactionCom />
      </div>
    </div>
  </div>
</div>