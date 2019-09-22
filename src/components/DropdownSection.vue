<template>
  <div :class="['dropdownSection', ...classes]" data-dropdown="products">
    <div class="dropdownContent" ref="content">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "DropdownSection",
  data() {
    return {
      active: false,
      classes: []
    }
  }
  // methods: {
  //   activate() {
  //     [0].$el.classList.add("active");
  //   }
  // }
};
</script>

<style></style>
