<script lang="ts">
export interface NativeDialogContentProps extends PrimitiveProps {}

export type NativeDialogContentEmits = {
  'pointerDownOutside': [event: PointerEvent]
}
</script>

<script setup lang="ts">
import { Primitive, type PrimitiveProps } from '@/Primitive'
import { injectNativeDialogContext } from './NativeDialogRoot.vue'

defineOptions({ inheritAttrs: false })

const emit = defineEmits<NativeDialogContentEmits>()

const context = injectNativeDialogContext()
</script>

<template>
  <dialog
    :id="context.dialogId"
    :ref="(el) => {
      context.dialogElement.value = el as HTMLDialogElement
    }"
    style="background: transparent"
    @close="context.open.value = false"
    @pointerdown.capture="(event) => {
      if (context.modal && event.target === context.dialogElement.value) {
        emit('pointerDownOutside', event)
      }
    }"
  >
    <Primitive v-bind="{ ...$props, ...$attrs }">
      <slot />
    </Primitive>
  </dialog>
</template>
