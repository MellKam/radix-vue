<script lang="ts">
import { createContext, useId } from '@/shared'
import { type Ref, ref, toRef, watch } from 'vue'

interface NativeDialogContext {
  open: Ref<boolean>
  modal: Readonly<Ref<boolean>>
  dialogElement: Ref<HTMLDialogElement | undefined>
  triggerElement: Ref<HTMLElement | undefined>
  dialogId: string
}

export const [injectNativeDialogContext, provideNativeDialogContext] = createContext<NativeDialogContext>('NativeDialogRoot')

export interface NativeDialogProps {
  open?: boolean
  modal?: boolean
}

export type NativeDialogEmits = {
  'update:open': [newOpenState: boolean]
}
</script>

<script setup lang="ts">
const props = withDefaults(defineProps<NativeDialogProps>(), {
  modal: true,
})

defineEmits<NativeDialogEmits>()

const open = defineModel<boolean>('open', { default: false })

const dialogElement = ref<HTMLDialogElement>()
const triggerElement = ref<HTMLElement>()

watch(open, (newOpenState) => {
  if (!dialogElement.value) {
    console.warn('No dialog element found. Make sure you are rendering the NativeDialogRoot component.')
    return
  }

  if (newOpenState === true)
    return props.modal ? dialogElement.value.showModal() : dialogElement.value.show()

  dialogElement.value.close()
})

provideNativeDialogContext({
  open,
  modal: toRef(() => props.modal),
  dialogId: useId(undefined, 'radix-vue-native-dialog-content'),
  dialogElement,
  triggerElement,
})
</script>

<template>
  <slot />
</template>
