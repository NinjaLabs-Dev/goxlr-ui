<script>
export default {
  name: "ContentContainer",
  props: {
    noLeftPad: Boolean,
  },
  methods: {
    handleScroll(event) {
      const target = event.target;

      // Check if the current element has the scroll class
      let isWithinScrollDiv = false;
      let element = target;
      while (element) {
        if (element.classList.contains('scroll') || element.classList.contains('sliderBox')) {
          isWithinScrollDiv = true;
          break;
        }
        element = element.parentElement;
      }

      if (!isWithinScrollDiv) {
        // Scroll container to the left or right
        this.$el.scrollLeft += event.deltaY;
      }
    }
  },
}
</script>

<template>
  <div class="container" :class="{ contentPadNoLeft: noLeftPad }" @wheel="handleScroll">
    <slot></slot>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.container {
  display: flex;
  flex-direction: row;
  gap: 15px;

  padding: 40px;

  overflow-x: scroll;
  overflow-y: hidden;
}

.container::-webkit-scrollbar {
  height: 6px;
  width: 6px;
}

.container::-webkit-scrollbar-track {
  background-color: transparent;
}

.container::-webkit-scrollbar-thumb {
  background-color: #dfdfdf;
  border-radius: 3px;
}

.contentPadNoLeft {
  padding-left: 0;
}
</style>
