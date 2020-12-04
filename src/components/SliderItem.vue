<template>
  <div id="SliderItem">
    <div class="item__description">
      <div class="item__name">{{slide.nemotecnico}}:</div>
      <div class="item__amount">{{slide.valor}}</div>
      <!--<div class="item__amount">{{slide.valor}}</div>-->
    </div>
    <div class="item__variation">
      <div class="item__variation__label">VAR %:</div>
      <!--{{slide.variacion_porcentaje | round(2)}}%-->
      <div :class="trend(slide.variacion_porcentaje)">{{slide.variacion_porcentaje}}%</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SliderItem',
  props: {
    slide: [Object, Array]
  },
  methods: {
    trend(value) {
      if (value > 0) {
        return 'item__variation__number item__variation__number--state-green';
      } else if (value < 0) {
        return 'item__variation__number item__variation__number--state-red';
      } else {
        return 'item__variation__number item__variation__number--state-gray';
      }
    }
  },
  filters: {
    currencyFormat: function(value) {
      var formatted = value
        .toFixed(2)
        .replace(/(\d)(?=(\d\d\d)+(?!\d))/g, '$1,');
      return formatted;
    },
    round: function(value, decimal) {
      // value = (Math.round(value * 100) / 100).toFixed(decimal);
      value = value.toFixed(decimal);
      return value;
    }
  }
};
</script>

<style scoped>
#SliderItem {
  font-size: 50px;
  width: 640px;
  display: flex;
  flex-direction: column;
}

.item__description {
  font-size: 60px;
  display: flex;
  justify-content: center;
  padding-bottom: 20px;
}

.item__name {
  display: inline-flex;
  color: #d9cfb1;
  padding-right: 10px;
}

.item__amount {
  display: inline-flex;
}

.item__variation {
  font-size: 55px;
  margin: 0 auto;
  padding-bottom: 5px;
  display: flex;
  align-items: center;
}

.item__variation__label {
  color: #c0c0c0;
  margin: auto;
  padding-right: 10px;
  align-self: center;
}

.item__variation__number {
  font-size: 40px;
  margin: auto;
  font-weight: 900;
  align-self: center;
}

.item__variation__number--state-red {
  background-color: #f3484d;
  border-radius: 20px;
  text-align: center;
  padding: 7px 7px 2px 7px;
}

.item__variation__number--state-green {
  background-color: #90a96d;
  border-radius: 20px;
  text-align: center;
  padding: 7px 7px 2px 7px;
}

.item__variation__number--state-gray {
  background-color: #464646;
  border-radius: 20px;
  text-align: center;
  padding: 7px 7px 2px 7px;
}
</style>