<script setup lang="ts">
  import { useTemplateRef } from 'vue'
  const dialogRef = useTemplateRef<HTMLDialogElement>('custom-dialog');

  const isDialog = (input: unknown): input is HTMLDialogElement => {
    return input instanceof HTMLDialogElement;
  };

  const showDialog = (): void => {
    const customDialog = dialogRef.value;
    if (!isDialog(customDialog)) return;
    customDialog.showModal();
  };

  const closeDialog = (): void => {
    const customDialog = dialogRef.value;
    if (!isDialog(customDialog)) return;
    customDialog.close();
  };
</script>

<template>
  <button aria-label="this is a button" @click="showDialog" border-none px-3 py-2 rounded-md cursor-pointer box-border text="hover:white" bg="blue-400 hover:blue-800">show</button>

  <dialog ref="custom-dialog" overflow-hidden rounded-md shadow-lg w="1/3" min-h="30vh">
    <section flex="~ col" items-center justify-center px-4 py-3 relative>
      <h2 absolute top-0 left-0 px-4 py-3 text-2xl font-bold w-full bg-blue-400 flex items-center>
        <span>
          Hello
        </span>
        <span role="button" @click="closeDialog" ml-auto font-bolder text-lg>&times;</span>
      </h2>
      <div mt-11 p="30%" w-full h-full flex items-center justify-center>
        <button aria-label="this is a button" @click="closeDialog" border-none px-3 py-2 rounded-md cursor-pointer box-border text="hover:white" bg="blue-400 hover:blue-800">close</button>
      </div>
    </section>
  </dialog>

</template>

<style lang="postcss">
html, body {
  padding: 0;
  margin: 0;
}

* {
  box-sizing: border-box;
  @apply font-mono;
}
</style>
