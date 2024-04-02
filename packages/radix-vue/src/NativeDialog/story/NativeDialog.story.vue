<script setup lang="ts">
import { ref } from 'vue'
import { NativeDialogClose, NativeDialogContent, NativeDialogPortal, NativeDialogRoot, NativeDialogTrigger } from '..'

const isOpen = ref(false)
</script>

<template>
  <Story title="NativeDialog/Demo" :layout="{ type: 'single', iframe: false }">
    <Variant title="default">
      Dialog open: {{ isOpen }}
      <NativeDialogRoot v-model:open="isOpen" :modal="false">
        <NativeDialogTrigger>
          Open dialog
        </NativeDialogTrigger>
        <NativeDialogPortal>
          <NativeDialogContent class="p-5 rounded-lg bg-white" @pointer-down-outside="isOpen = false">
            Hello, world!
            <NativeDialogClose>
              X
            </NativeDialogClose>
          </NativeDialogContent>
        </NativeDialogPortal>
      </NativeDialogRoot>
    </Variant>
  </Story>
</template>
