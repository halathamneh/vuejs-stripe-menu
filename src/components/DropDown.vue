<template>
  <div
    class="dropdownRoot"
    @mouseenter="$emit('mouseenter', $event)"
    @mouseleave="$emit('mouseleave', $event)"
  >
    <div
      class="dropdownBackground"
      :style="{ transform: bgTransform }"
      ref="section-bg"
    ></div>
    <div
      class="dropdownArrow"
      ref="dropdown-arrow"
    ></div>
    <div class="dropdownContainer" :style="{ transform: containerTransform, width: containerWidth, height: containerHeight }">
      <dropdown-section
        v-for="(item, index) in config.primary"
        :key="index"
        :class="{
          left: currentDropdown.index > index,
          active: currentDropdown.index === index,
          right: currentDropdown.index < index
        }"
        :ref="'dropdown-' + item.name"
      >
        <div style="width: 450px; height: 350px;" v-if="item.name === 'products'">
          <h2 style="font-size: 28px;margin-bottom: 20px;">Products</h2>
          <p style="font-size: 16px;">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias assumenda expedita fugiat, neque nobis recusandae repudiandae! Accusamus amet esse fugiat laudantium minus officia, tempora velit vitae voluptatem! Assumenda fugit, sequi.</p>
        </div>
        <div style="width: 250px; height: 250px;" v-if="item.name === 'developers'">
          <h2 style="font-size: 28px;margin-bottom: 20px;">Developers</h2>
          <p style="font-size: 16px;">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias assumenda expedita fugiat, neque nobis recusandae repudiandae! Accusamus amet esse fugiat laudantium minus officia, tempora velit vitae voluptatem! Assumenda fugit, sequi.</p>
        </div>
        <div style="width: 350px; height: 200px;" v-if="item.name === 'company'">
          <h2 style="font-size: 28px;margin-bottom: 20px;">Company</h2>
          <p style="font-size: 16px;">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias assumenda expedita fugiat, neque nobis recusandae repudiandae! Accusamus amet esse fugiat laudantium minus officia, tempora velit vitae voluptatem! Assumenda fugit, sequi.</p>
        </div>
      </dropdown-section>
    </div>
  </div>
</template>

<script>
import DropdownSection from "@/components/DropdownSection";
export default {
  name: "DropDown",
  components: { DropdownSection },
  data() {
    return {
      bgTransform: "",
      containerTransform: "",
      containerWidth: 0,
      containerHeight: 0,
    };
  },
  props: {
    currentDropdown: Object,
    config: Object
  },
  methods: {
    setPosition() {
      const { element } = this.currentDropdown,
              sectionBg = this.$refs["section-bg"];
      let elementRect = element.getBoundingClientRect();
      const { name } = this.currentDropdown,
              sectionContent = this.$refs[`dropdown-${name}`],
              rect = sectionContent[0].$refs['content'].getBoundingClientRect();
      this.containerWidth = `${rect.width}px`;
      this.containerHeight = `${rect.height}px`;
      let scaleX = rect.width / parseInt(getComputedStyle(sectionBg).width),
              scaleY = rect.height / parseInt(getComputedStyle(sectionBg).height),
       leftPos = elementRect.left + (elementRect.width /2) - (rect.width / 2);
      this.bgTransform = `translateX(${leftPos}px) scaleX(${scaleX}) scaleY(${scaleY})`;
      this.containerTransform = `translateX(${leftPos}px)`;
      this.setArrowPos(elementRect.left + elementRect.width / 2);
    },
    show() {

    },
    setArrowPos(left) {
      const arrow = this.$refs["dropdown-arrow"];
      // left -= arrow.getBoundingClientRect().width / 2;
      arrow.style.transform = `translateX(${left}px) rotate(45deg)`;
    }
  }
};
</script>

<style></style>
