<template>
  <div class="main" :class="{ 'p8': perspectiveCount == 8, 'p4': perspectiveCount == 4, 'p2': perspectiveCount == 2, }">
    <div class="scroller">
      <div class="scrolling-text">{{ times }}</div>
    </div>
    <div class="vid" v-if="ch1">
      <iframe :src="twitchUrl(ch1)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch2">
      <iframe :src="twitchUrl(ch2)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch3">
      <iframe :src="twitchUrl(ch3)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch4">
      <iframe :src="twitchUrl(ch4)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch5">
      <iframe :src="twitchUrl(ch5)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch6">
      <iframe :src="twitchUrl(ch6)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch7">
      <iframe :src="twitchUrl(ch7)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>
    <div class="vid" v-if="ch8">
      <iframe :src="twitchUrl(ch8)" frameborder="0" allowfullscreen="true" scrolling="no" muted="true"></iframe>
    </div>

    <div class="vid" v-if="ch9">
      <!-- <div class="game-chat">
        <label>Match Log</label>
      </div> -->
      <h1>commentators</h1>
    </div>
  </div>
  <div class="side-bar">
    <div style="margin-top: 20px;">
      <div class="channel">
        1:
        <input type="text" v-model="ch1" />
        <select @change="changeChannel($event, 1)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        2:
        <input type="text" v-model="ch2" />
        <select @change="changeChannel($event, 2)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        3:
        <input type="text" v-model="ch3" />
        <select @change="changeChannel($event, 3)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        4:
        <input type="text" v-model="ch4" />
        <select @change="changeChannel($event, 4)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        5:
        <input type="text" v-model="ch5" />
        <select @change="changeChannel($event, 5)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        6:
        <input type="text" v-model="ch6" />
        <select @change="changeChannel($event, 6)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        7:
        <input type="text" v-model="ch7" />
        <select @change="changeChannel($event, 7)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
      <div class="channel">
        8:
        <input type="text" v-model="ch8" />
        <select @change="changeChannel($event, 8)">
          <option value="">---</option>
          <option v-for="r in runners" v-bind:key="r.id" v-bind:value="r">{{ r }}</option>
        </select>
      </div>
    </div>
    <textarea v-model="times"></textarea>


  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data: () => {
    return {
      ch1: "",
      ch2: "",
      ch3: "",
      ch4: "",
      ch5: "",
      ch6: "",
      ch7: "",
      ch8: "",
      ch9: "",

      runnersRaw: "21mashedpotatoes;7rowl;acerpx_;blakwolf_;blyde19;cooshw;cropro;cube1337x;dougthepig;doypingu;eficzz;feinberg;fudge1;fyroah;nwolcjosh;leonn_aa;averageaaplayer;marieee824;meistermaki;nicetwice;oxidiot;queenkac;ravalle;superc__;taffellive;thatstigerr",
      runners: [],

      cols: 3,
      rows: 3,
      pad: "10px 20px",
      padTopBottom: 10,
      padLeftRight: 20,
      width: 600,
      height: 340,

      perspectiveCount: 8,

      times: "Feinberg - 2:38, DoyPingu - 3:01, QueenKac - 3:03"
    }
  },
  created() {
    this.runners = this.runnersRaw.split(";");

    this.ch1 = this.runners[0];
    this.ch2 = this.runners[1];
    this.ch3 = this.runners[2];
    this.ch4 = this.runners[3];
    this.ch5 = this.runners[4];
    this.ch6 = this.runners[5];
    this.ch7 = this.runners[6];
    this.ch8 = this.runners[7];
  },
  methods: {
    twitchUrl(name) {
      return `https://player.twitch.tv/?channel=${name}&parent=localhost`;
    },
    calculateSize() {
      this.width = (1920 / this.cols) - (this.padLeftRight * 2);
      this.height = (1080 / this.rows) - (this.padTopBottom * 2);
      this.pad = `${this.padTopBottom}px ${this.padLeftRight}px`;
    },
    changeChannel(evt, id) {
      var val = evt.target.value;
      switch (id) {
        case 1:
          this.ch1 = val;
          break;
        case 2:
          this.ch2 = val;
          break;
        case 3:
          this.ch3 = val;
          break;
        case 4:
          this.ch4 = val;
          break;
        case 5:
          this.ch5 = val;
          break;
        case 6:
          this.ch6 = val;
          break;
        case 7:
          this.ch7 = val;
          break;
        case 8:
          this.ch8 = val;
          break;
        case 9:
          this.ch9 = val;
          break;
      }
      evt.target.value = "";
    }
  }
}
</script>

<style>
@import url('https://fonts.cdnfonts.com/css/minecraft-4');

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-color: #333;
}

.main {
  width: 1920px;
  height: 1080px;
  float: left;
  position: relative;

  margin-right: 10px;
  background-color: #000;
}

.vid {
  float: left;
  width: 640px;
  height: 350px;
  transition: 0.3s ease-in-out;
}

.scroller {
  height: 30px;
  background: #000;
  color: #FFF;
  font-family: 'Minecraft', sans-serif;
  text-shadow: 1px 1px 1px #333;
  font-size: 24px;
  letter-spacing: 5px;
  overflow: hidden;
}

.vid.zoom {
  width: 1240px;
  height: 700px;
  background-color: pink;
}

.green-screen {
  background-color: green;
  height: 100%;
  width: 100%;
}

.options {
  padding: 10px 0;
}

.side-bar {
  float: left;
  width: 500px;
  border: 1px solid black;
  padding: 10px;
}

.side-bar label {
  display: block;
}

.half {
  width: 50%;
  float: left;
}



.clear {
  clear: both;
}

.channel {
  padding: 5px 0;
}

.channel select {
  width: 100px;
}

.channel select,
.channel button {
  margin-left: 10px;
}

.vid iframe {
  width: 100%;
  height: 100%;
  ;
}

.main.p4 .vid {
  width: 800px;
  height: 450px;
  margin-bottom: 140px;
}

.main.p4 .vid:nth-child(2n) {
  margin-left: 260px;
}

.main.p2 {
  box-sizing: border-box;
}

.main.p2 .vid {
  width: 920px;
  height: 516px;
  margin: 260px 20px;
}

.game-chat {
  font-family: 'Minecraft', sans-serif;
  background-color: #222;
  width: 100%;
  height: 100%;
  border: 10px solid darkcyan;
  text-align: center;
}

.game-chat label {
  display: block;
  background-color: darkcyan;
  padding-bottom: 10px;
  color: #ccc;
  font-size: 20px;
  text-shadow: 1px 1px 1px #00000099;
}


.scrolling-text {
  /* animation properties */
  -moz-transform: translateX(100%);
  -webkit-transform: translateX(100%);
  transform: translateX(100%);

  -moz-animation: my-animation 60s linear infinite;
  -webkit-animation: my-animation 60s linear infinite;
  animation: my-animation 60s linear infinite;
}

/* for Firefox */
@-moz-keyframes my-animation {
  from { -moz-transform: translateX(100%); }
  to { -moz-transform: translateX(-100%); }
}

/* for Chrome */
@-webkit-keyframes my-animation {
  from { -webkit-transform: translateX(100%); }
  to { -webkit-transform: translateX(-100%); }
}

@keyframes my-animation {
  from {
    -moz-transform: translateX(100%);
    -webkit-transform: translateX(100%);
    transform: translateX(100%);
  }
  to {
    -moz-transform: translateX(-100%);
    -webkit-transform: translateX(-100%);
    transform: translateX(-100%);
  }
}
</style>
