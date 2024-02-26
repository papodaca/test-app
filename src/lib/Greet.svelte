<script>
  import { invoke } from "@tauri-apps/api/core"
  import { open } from '@tauri-apps/plugin-dialog'

  let name = "";
  let greetMsg = ""

  async function greet(){
    // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
    greetMsg = await invoke("greet", { name })
    let files = await open({
    multiple: true,
    filters: [{
      name: "Image",
      extensions: ["png", "jpeg", "jpg", "webp", "bmp", "tiff", "gif"]
    }]
  })
  }
</script>

<div>
  <form class="row" on:submit|preventDefault={greet}>
    <input id="greet-input" placeholder="Enter a name..." bind:value={name} />
    <button type="submit">Greet</button>
  </form>
  <p>{greetMsg}</p>
</div>

