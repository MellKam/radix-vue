<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { type DateValue } from '@internationalized/date'

export interface CalendarCellProps extends PrimitiveProps {
  /** The date value for the cell */
  date: DateValue
}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { injectCalendarRootContext } from './CalendarRoot.vue'

const props = withDefaults(defineProps<CalendarCellProps>(), { as: 'td' })
const rootContext = injectCalendarRootContext()
</script>

<template>
  <Primitive
    role="gridcell"
    :as="props.as"
    :as-child="props.asChild"
    :aria-selected="rootContext.isDateSelected(date) ? true : undefined"
    :aria-disabled="rootContext.isDateDisabled(date) || rootContext.isDateUnavailable?.(date)"
    :data-disabled="rootContext.isDateDisabled(date) ? '' : undefined"
  >
    <slot />
  </Primitive>
</template>
