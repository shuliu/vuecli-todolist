<template>
  <div class="select">
    <select v-model="selectIndex" >
      <option v-for="(item, index) in options" :value="index">{{item.name}}</option>
    </select>

    <span v-if="showInfo()">{{selectIndex}}, {{selectName}}</span>
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
  data() {
    return {
      options: this.list,
      selectIndex: this.value,
      selectName: ''
    }
  },
  created() {
    this.selectName = this.options.length > 0 ? this.options[0].name : this.selectName;
  },
  computed: {
  },
  methods: {
    showInfo() {
      return this.selectName !== '';
    },
    getSelectName() {
      this.selectName = this.options.length > 0 ? this.options[this.selectIndex].name : '';
    },
  },
  watch: {
    selectIndex: ['getSelectName'],
  }
}
</script>

<style>

</style>
