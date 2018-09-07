<template>
  <div class="select">
    <select v-model="selectIndex" >
      <option v-for="(item, key) in list" :key="key" :value="key">{{item.name}}</option>
    </select>

    <span v-if="showInfo()">{{this.value}}, {{getSelectName()}}</span>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: function() { return []; }
    },
    value: Number
  },
  methods: {
    showInfo() {
      return this.list.length > 0;
    },
    getSelectName() {
      return this.list.length > 0 ? this.list[this.value].name : '';
    },
  },
  computed: {
    selectIndex: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit('input', val);
      }
    }
  },
  watch: {
    selectIndex: ['getSelectName'],
    list: ['getSelectName']
  }
}
</script>

<style>

</style>
