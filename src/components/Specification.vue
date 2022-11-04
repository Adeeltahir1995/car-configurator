<template>
  <div class="specification">
    <h3 @click="show = !show">{{ this.data.name }}</h3>
    <div v-if="show" class="specification__box">
      <div>Engine - {{ this.data.engine }}</div>
      <div>Seats - {{ this.data.seats }}</div>
      <div>Color - {{ this.data.color }}</div>
      <div>Tire Size - {{ this.data.tireSize }}</div>
      <div :key="option" v-for="(option, index) in this.data.options">
        <div>{{ option }} - {{ this.data.newData[index] }}</div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "Specification",
  props: {
    data: Array,
  },
  data() {
    return {
      show: false,
    };
  },
};
</script>

<style scoped lang="scss">
.specification {
  display: flex;
  flex-direction: column;
  gap: 16px;
  h3 {
    background: #eee;
    padding: 16px;
    border: 1px solid #eee;
    box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
    border-radius: 5px;
    cursor: pointer;
  }
  &__box {
    display: flex;
    flex-direction: column;
    gap: 8px;
    padding: 16px;
    border: 1px solid #eee;
    box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
    border-radius: 5px;
  }
}
</style>
