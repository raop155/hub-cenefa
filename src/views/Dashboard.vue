<template>
  <div id="dashboard">
    <MediaPlayer />
    <div class="sector">
      <MarqueeText :repeat="2" :duration="60" :key="key" :paused="false">
        <div class="marquee-item">
          <SliderItem v-for="item in sliders" :key="item.nemotecnico" :slide="item"></SliderItem>
        </div>
      </MarqueeText>
    </div>
    <div class="sector">
      <MarqueeText :repeat="2" :duration="60" :key="key" :paused="false">
        <div class="marquee-item">
          <SliderItem v-for="item in sliders2" :key="item.nemotecnico" :slide="item"></SliderItem>
        </div>
      </MarqueeText>
    </div>
    <div class="sector">
      <MarqueeText :repeat="2" :duration="60" :key="key" :paused="false">
        <div class="marquee-item">
          <SliderItem v-for="item in sliders3" :key="item.nemotecnico" :slide="item"></SliderItem>
        </div>
      </MarqueeText>
    </div>
  </div>
</template>

<script>
import MediaPlayer from '../components/MediaPlayer.vue';
import SliderItem from '../components/SliderItem.vue';

import MarqueeText from 'vue-marquee-text-component';
import axios from 'axios';

export default {
  name: 'dashboard',
  components: {
    MediaPlayer,
    SliderItem,
    MarqueeText
  },
  data: () => {
    return {
      token: null,
      timer: null,
      counter: 0,
      error: '',
      key: 'marquee',
      sliders: [],
      sliders2: [],
      sliders3: []
    };
  },
  mounted() {
    console.log('Dashboard mounted!');
    this.getToken();
    this.getSliderData();
    this.timer = setInterval(this.getToken, 60000 * 5);

    // process.env.NODE_ENV;
    console.log(
      'process.env.VUE_APP_VALOR_FUTURO_URL',
      process.env.VUE_APP_VALOR_FUTURO_URL
    );
  },
  methods: {
    getToken() {
      let headers = {
        headers: {
          'Content-type': 'text/plain'
        }
      };
      let params = 'UserName=bsantander&Password=Santand3R&grant_type=password';

      axios
        .post(
          process.env.VUE_APP_VALOR_FUTURO_URL + '/vftoken/oauth/token',
          params,
          headers
        )
        .then(response => {
          console.log(response.data);

          this.token = response.data.access_token;
          this.counter++;
        })
        .catch(error => {
          if (error.response) {
            console.log('data', error.response.data);
            //console.log('status', error.response.status);
            //console.log('headers', error.response.headers);
          }
          console.log('config', error.config);
        });

      console.log('counter', this.counter);
    },
    getSliderData() {
      let headers = {
        headers: {
          Authorization: 'Bearer ' + this.token
        }
      };

      let params = {};

      axios
        .post(
          process.env.VUE_APP_VALOR_FUTURO_URL +
            '/VFRest/api/Santander/DataSlider',
          params,
          headers
        )
        .then(response => {
          //console.log(response.data);

          if (JSON.stringify(this.sliders) !== JSON.stringify(response.data)) {
            this.sliders = response.data;
            console.log('Slider data change!');

            // Copy sliders array and reorder arrays
            let item;

            this.sliders2 = this.sliders.slice();
            item = this.sliders2.shift();
            this.sliders2.push(item);
            item = this.sliders2.shift();
            this.sliders2.push(item);
            item = this.sliders2.shift();
            this.sliders2.push(item);

            this.sliders3 = this.sliders.slice();
            item = this.sliders3.shift();
            this.sliders3.push(item);
            item = this.sliders3.shift();
            this.sliders3.push(item);
            item = this.sliders3.shift();
            this.sliders3.push(item);
            item = this.sliders3.shift();
            this.sliders3.push(item);
            item = this.sliders3.shift();
            this.sliders3.push(item);
            item = this.sliders3.shift();
            this.sliders3.push(item);
          } else {
            // console.log('They are equal!');
          }
          this.getSliderData();
        })
        .catch(error => {
          if (error.response) {
            console.log('data', error.response.data);
            //console.log('status', error.response.status);
            //console.log('headers', error.response.headers);
          }
          // console.log('config', error.config);
          this.getSliderData();
        });
    }
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style scoped>
#dashboard {
  width: 1920px;
  height: 1080px;
}

#data {
  position: relative;
}

.marquee-item {
  display: flex;
  height: 100%;
  width: 100%;
  color: white;
}

.sector {
  width: 100%;
  height: 33.333%;
  display: flex;
  align-items: center;
}
</style>
