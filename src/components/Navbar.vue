<template>
  <ul class="navRoot">
    <li class="navSection logo">
      <logo />
    </li>

    <li class="navSection primary" @mouseleave="$emit('hideDropdown')">
      <button
        v-for="(item, index) in config.primary"
        :key="index"
        :class="{
          rootLink: true,
          'item-products': true,
          hasDropdown: true,
          active: index === currentDropdown.index
        }"
        data-dropdown="products"
        @mouseenter="$emit('showDropdown', $event.target, item, index)"
      >
        {{ item.text }}
      </button>
    </li>

    <li class="navSection secondary">
      <a
        class="rootLink item-support"
        href="https://support.stripe.com"
      >
        Support
      </a>
      <a
        class="rootLink item-dashboard"
        data-adroll-segment="submit_two"
        href="https://dashboard.stripe.com/login"
      >
        Sign in
      </a>
    </li>

  </ul>
</template>

<script>
import Logo from "@/components/Logo";
export default {
  name: "Navbar",
  components: { Logo },
  props: {
    config: Object,
    currentDropdown: Object
  }
};
</script>

<style></style>
