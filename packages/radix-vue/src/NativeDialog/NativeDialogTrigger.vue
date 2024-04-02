<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface NativeDialogTriggerProps extends PrimitiveProps { }
</script>

<script setup lang="ts">
import { injectNativeDialogContext } from './NativeDialogRoot.vue'
import { Primitive } from '@/Primitive'

const props = defineProps<NativeDialogTriggerProps>()

const context = injectNativeDialogContext()
</script>

<template>
  <Primitive
    :as="props.as || 'button'"
    :as-child="props.asChild"
    :type="props.as === 'button' ? 'button' : undefined"
    aria-haspopup="dialog"
    :aria-expanded="context.open.value"
    :aria-controls="context.open.value ? context.dialogId : undefined"
    :data-state="context.open.value ? 'open' : 'closed'"
    @click="context.open.value = true"
  >
    <slot />
  </Primitive>
</template>
