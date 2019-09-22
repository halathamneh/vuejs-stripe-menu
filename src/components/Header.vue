<template>
  <header
    :class="{
      globalNav: true,
      noDropdownTransition,
      dropdownActive,
      overlayActive: dropdownActive
    }"
  >
      <div id="stripes" aria-hidden="true"></div>
    <div class="container-lg">
      <navbar
        :config="navbar_config"
        v-on:showDropdown="(e, item, index) => updateCurrentDropdown(e, item, index)"
        v-on:hideDropdown="hideDropdown"
        :current-dropdown="currentDropdown"
      />
      <drop-down
        ref="dropdown"
        :config="navbar_config"
        :current-dropdown="currentDropdown"
        @mouseenter="stopTimeout"
        @mouseleave="hideDropdown"
      />
    </div>
  </header>
</template>

<script>
import Navbar from "@/components/Navbar";
import navbar_config from "../../navbar_config";
import DropDown from "@/components/DropDown";

let timeOut = false,
  duration = 100;
export default {
  name: "Header",
  components: { DropDown, Navbar },
  data() {
    return {
      navbar_config,
      currentDropdown: {
        element: null,
        name: null,
          index: -1
      },
      dropdownActive: false,
      noDropdownTransition: true
    };
  },
  methods: {
    updateCurrentDropdown(element, item, index) {
      this.stopTimeout();
      this.currentDropdown.element = element;
      this.currentDropdown.name = item.name;
      this.currentDropdown.index = index;
      const dropDown = this.$refs["dropdown"];
      dropDown.setPosition();
      dropDown.show();
      this.dropdownActive = true;
      setTimeout(() => {
        this.noDropdownTransition = false;
      }, 100);
    },
    hideDropdown() {
      timeOut = setTimeout(() => {
        this.dropdownActive = false;
        this.noDropdownTransition = true;
        this.currentDropdown.name = null;
        this.currentDropdown.index = -1;
      }, duration);
    },
    stopTimeout() {
      clearTimeout(timeOut);
    }
  }
};
</script>

<style></style>
