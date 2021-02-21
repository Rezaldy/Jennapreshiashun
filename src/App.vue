<template>
  <div id="q-app"
       class="app"
       :class="{
      morning : periodOfDay === 'morning',
      lateMorning : periodOfDay === 'lateMorning',
      afternoon : periodOfDay === 'afternoon',
      lateAfternoon : periodOfDay === 'lateAfternoon',
      evening : periodOfDay === 'evening',
      lateEvening : periodOfDay === 'lateEvening',
      night : periodOfDay === 'night',
      lateNight : periodOfDay === 'lateNight',
    }">
    <router-view />
  </div>
</template>
<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import moment from 'moment-timezone'

@Component
export default class App extends Vue {
  get timezone () {
    return Intl.DateTimeFormat().resolvedOptions().timeZone
  }

  get currentTime () {
    // eslint-disable-next-line @typescript-eslint/no-unsafe-call,@typescript-eslint/no-unsafe-return
    return moment().tz(this.timezone).hours()
  }

  get periodOfDay () {
    /**
     * Morning 6 - 10
     * Late Morning 10 - 12
     * Afternoon 12 - 15
     * Late Afternoon 15 - 18
     * Evening 18 - 21
     * Late Evening 21-00
     * Night 0 - 3
     * Late Night 3 - 6
     */
    const currentTime = this.currentTime

    switch (true) {
      case currentTime >= 6 && currentTime < 10:
        return 'morning'
      case currentTime >= 10 && currentTime < 12:
        return 'lateMorning'
      case currentTime >= 12 && currentTime < 15:
        return 'afternoon'
      case currentTime >= 15 && currentTime < 18:
        return 'lateAfternoon'
      case currentTime >= 18 && currentTime < 21:
        return 'evening'
      case currentTime >= 21:
        return 'lateEvening'
      case currentTime >= 0 && currentTime < 3:
        return 'night'
      case currentTime >= 3 && currentTime > 6:
        return 'lateNight'
    }
  }
}
</script>

<style lang="scss" scoped>
.morning {
  background-image: url("~assets/images/bg/morning.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.lateMorning {
  background-image: url("~assets/images/bg/lateMorning.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.afternoon {
  background-image: url("~assets/images/bg/afternoon.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.lateAfternoon {
  background-image: url("~assets/images/bg/lateAfternoon.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.evening {
  background-image: url("~assets/images/bg/evening.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.lateEvening {
  background-image: url("~assets/images/bg/lateEvening.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.night {
  background-image: url("~assets/images/bg/night.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.lateNight {
  background-image: url("~assets/images/bg/lateNight.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.app {
  &:after {
    content: '\A';
    position: absolute;
    width: 100%; height:100%;
    top:0; left:0;
    background:rgba(0,0,0,.3);
  }
}
</style>

<style lang="scss">
.q-layout {
  z-index:5;
}
</style>
