<script>
  export let pokemon = 'Pokemon',
    level = null,
    submit = (_) => _

  import { getContext } from 'svelte'

  import { Button, IconButton, Input } from '$c/core'
  import { X } from '$icons'

  const { close } = getContext('simple-modal')

  let value = level ?? null

  const save = () => {
    const parsed = Number(value)
    const nextLevel =
      Number.isFinite(parsed) && parsed >= 1 && parsed <= 100
        ? Math.floor(parsed)
        : null

    submit(nextLevel)
    close()
  }
</script>

<section
  class="mx-auto w-full max-w-sm rounded-2xl bg-gray-50 p-6 shadow-lg dark:bg-gray-900 dark:text-gray-50"
>
  <div class="mb-4 flex items-start justify-between gap-x-4">
    <div>
      <h2 class="text-lg font-bold">Track Level</h2>
      <p class="text-sm text-gray-600 dark:text-gray-400">
        Save the current level for <b>{pokemon}</b>.
      </p>
    </div>

    <IconButton
      rounded
      borderless
      color="orange"
      containerClassName="-mt-1"
      src={X}
      on:click={close}
      title="Close modal"
    />
  </div>

  <Input
    rounded
    type="number"
    min={1}
    max={100}
    bind:value
    name="{pokemon} Level"
    placeholder="Level"
    className="mb-4"
  />

  <div class="flex flex-row-reverse gap-2">
    <Button rounded solid className="flex-1" on:click={save}>
      <small>Save level</small>
    </Button>
    <Button rounded className="flex-1" on:click={close}>
      <small>Skip</small>
    </Button>
  </div>
</section>
