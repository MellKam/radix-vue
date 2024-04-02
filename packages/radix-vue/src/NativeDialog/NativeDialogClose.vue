<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface NativeDialogCloseProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { injectNativeDialogContext } from './NativeDialogRoot.vue'
import { Primitive } from '@/Primitive'

const props = withDefaults(defineProps<NativeDialogCloseProps>(), {
  as: 'button',
})

const context = injectNativeDialogContext()
</script>

<template>
  <Primitive
    v-bind="props"
    :type="as === 'button' ? 'button' : undefined"
    @click="context.open.value = false"
  >
    <slot />
  </Primitive>
</template>
