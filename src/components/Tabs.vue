<template>
  <div v-if="tabs && tabs.length > 1" class="homer-tabs">
    <ul>
      <li
        v-for="tab in tabs"
        :key="tab.name"
        :class="{ 'is-active': currentTab === (tab.config || tab.name.toLowerCase().replace(/\s+/g, '-')) }"
      >
        <a @click.prevent="switchTab(tab)">
          <i v-if="tab.icon" :class="tab.icon"></i>
          {{ tab.name }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Tabs",
  props: {
    tabs: {
      type: Array,
      default: () => [],
    },
    currentTab: {
      type: String,
      default: "default",
    },
  },
  emits: ["tab-change"],
  methods: {
    switchTab(tab) {
      const hash = tab.config || tab.name.toLowerCase().replace(/\s+/g, "-");
      window.location.hash = hash === "default" ? "" : hash;
      this.$emit("tab-change", tab.name);
    },
  },
};
</script>

<style scoped>
.homer-tabs {
  background: var(--highlight-primary, #3367d6);
  padding: 0 1.5rem;
}

.homer-tabs ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 6px;
  align-items: flex-end;
}

.homer-tabs li a {
  display: block;
  padding: 0.6rem 1.4rem;
  color: rgba(255, 255, 255, 0.75);
  font-weight: 500;
  font-size: 0.9rem;
  border-radius: 6px 6px 0 0;
  transition: all 0.2s ease;
  cursor: pointer;
  text-decoration: none;
  margin-top: 8px;
}

.homer-tabs li a:hover {
  color: #ffffff;
  background: rgba(255, 255, 255, 0.15);
}

.homer-tabs li.is-active a {
  background: #ffffff;
  color: #363636;
  font-weight: 700;
}

.homer-tabs li a i {
  margin-right: 6px;
}
</style>
