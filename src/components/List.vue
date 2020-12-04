<template>
  <div class="list">
    <div class="tituloIND">
      <div class="tituloempresa">{{title}}:</div>
      <div class="tituloultimo">ÚLTIMO:</div>
      <div class="titulovariabilidad">VARIABILIDAD:</div>
    </div>
    <!--------END-TITULOIND------->
    <div class="list">
      <div class="indices" v-for="item in items" :key="item.nemotecnico">
        <div class="empresa item">{{item.nemotecnico}}</div>
        <div class="flechaAMA item"></div>
        <div class="ultimo item">-</div>
        <div class="variabilidad item">
          <div :class="trend(item.variacion_porcentaje)">{{item.variacion_porcentaje | round(2)}}%</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'list',
  props: {
    title: String,
    items: [Array, Object]
  },
  data: () => {
    return {
      test: null
    };
  },
  methods: {
    trend(value) {
      if (value > 0) {
        return 'alzas';
      } else if (value < 0) {
        return 'bajas';
      } else {
        return 'neutral';
      }
    }
  },
  filters: {
    round: function(value, decimal) {
      // value = (Math.round(value * 100) / 100).toFixed(decimal);
      value = value.toFixed(decimal);
      return value;
    }
  },
  updated: function() {
    console.log('List updated!', this.title);
  }
};
</script>

<style scoped>
.list {
}

.tituloIND {
  width: 400px;
  height: 23px;
  background-color: #353534;
  display: flex;
  align-items: center;
  font-size: 12px;
  color: #959595;
  margin-bottom: 10px;
}

.tituloempresa {
  width: 200px;
  height: 23px;
  background-color: #999999;
  color: #353534;
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 2;
}
.tituloultimo {
  width: 140px;
  text-align: center;
  flex: 1;
}
.titulovariabilidad {
  text-align: center;
  flex: 1;
}

.indices {
  height: 35px;
  font-size: 17px;
  font-family: 'DIN_medium';
  color: #fff;
  display: flex;
  justify-content: space-evenly;
}

.item {
  flex: 1;
  align-self: center;
}

.empresa {
}
.flechaAMA {
  height: 33px;
  width: 30px;
  background-image: url(../assets/flecha_amarillo.png);
  background-position: center;
  background-repeat: no-repeat;
}
.ultimo {
  text-align: center;
}
.variabilidad {
}
.alzas {
  font-size: 15px;
  width: 70px;
  height: 28px;
  background-color: #93b367;
  border-radius: 20px;
  text-align: center;
  line-height: 28px;
  margin: 0 auto;
}
.bajas {
  font-size: 15px;
  width: 70px;
  height: 28px;
  background-color: #f3484d;
  border-radius: 20px;
  text-align: center;
  line-height: 28px;
  margin: 0 auto;
}

.neutral {
  font-size: 15px;
  width: 70px;
  height: 28px;
  background-color: #ccc;
  border-radius: 20px;
  text-align: center;
  line-height: 28px;
  margin: 0 auto;
}
</style>