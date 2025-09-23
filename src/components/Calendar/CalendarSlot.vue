<template>
  <component v-if="slot" :is="slot" v-bind="attrs" />
  <slot v-else />
</template>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<script setup lang="ts">
import { useAttrs } from 'vue';
import { useSlot } from '../../use/slots';

export type CalendarSlotName =
  | 'day-content'
  | 'day-popover'
  | 'dp-footer'
  | 'footer'
  | 'header-title-wrapper'
  | 'header-title'
  | 'header-prev-button'
  | 'header-next-button'
  | 'nav'
  | 'nav-prev-button'
  | 'nav-next-button'
  | 'page'
  | 'time-header';

const props = defineProps<{
  name: CalendarSlotName;
}>();

// Ensure attrs is not inferred as {} which can cause 'never' issues in template bindings
const attrs = useAttrs() as Record<string, any>;

// Cast slot to a broad type so dynamic component resolution accepts it
const slot = useSlot(props.name) as any;
</script>
