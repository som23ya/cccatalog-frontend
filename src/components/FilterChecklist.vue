<template>
  <fieldset>
    <div class="filters-title" @click.prevent="toggleFilterVisibility">
      <span>{{ title }}</span>

      <button class="filter-dropdown-visibility-button">
        <img src="@/assets/arrow-bottom.svg" class="arrow-bottom" alt="toggle filters visibility" />
      </button>
    </div>

    <div v-for="(item, index) in options" :key="index" v-if="filtersVisible">
      <input type="checkbox"
             class="filter-checkbox"
             :id="item.code"
             :key="index"
             :checked="item.checked"
             :disabled="disabled"
             @change="onValueChange" />
      <label class="filter-label" :for="item.code">{{ item.name }}</label>
    </div>
  </fieldset>
</template>

<script>
export default {
  name: 'filter-check-list',
  props: ['options', 'title', 'filterType', 'disabled'],
  data() {
    return { filtersVisible: false };
  },
  methods: {
    onValueChange(e) {
      this.$emit('filterChanged', { code: e.target.id, filterType: this.$props.filterType });
    },
    toggleFilterVisibility() {
      this.filtersVisible = !this.filtersVisible;
    },
  },
};
</script>

<style lang="scss" scoped>
fieldset {
  padding-left: 24px;
  padding-right: 34px;
  border-bottom: 1px solid #d8d8d8;
  margin-top: 20px;
  margin-bottom: 10px;
}

.filters-title {
  font-size: 1.250em;
  font-weight: 600;
  font-stretch: normal;
  font-style: normal;
  line-height: 1.5;
  letter-spacing: normal;
  cursor: pointer;
  margin-bottom: 16px;
}

.filter-dropdown-visibility-button {
  float: right;
  cursor: pointer;
}

label {
  color: #333333;
}
</style>
