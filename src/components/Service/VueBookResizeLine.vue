<template>
  <div class="vue-book-resize-line"
       :class="{'vue-book-resize-line--is-horizontal': isHorizontal}"
       draggable
       @drag="onDrag"
  />
</template>

<script lang="ts">

export default {
  data () {
    return {
      startValue: 0,
      startCoordinate: 0,
    }
  },
  props: {
    value: {
      type: Number,
      required: true,
    },
    isHorizontal: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onDrag (event: DragEvent): void {
      // No idea how, but this works.
      if (this.isHorizontal) {
        if (event.screenY) {
          const totalHeight = document.documentElement.clientHeight
          this.$emit('input', totalHeight - (event.clientY))
        }
        return
      }

      if (event.screenX) {
        this.$emit('input', event.clientX)
      }
    },
  },
}
</script>

<style lang="scss">
@import "../../scss/resources";

.vue-book-resize-line {
  width: 4px;
  cursor: col-resize;
  &--is-horizontal {
    cursor: row-resize;
  }
}
</style>