<template>
  <div class="main">
    <div class="test-pack columns">
      <div class="diaper-images column">
        <img v-bind:src="require(`@/${imgDir}/${selectedTestPack.images.trial_pack}`)">
      </div>
      <div class="test-packages column">
        <h2>Our Free Test Package</h2>
        <p style="text-transfor: uppercase;">choose your size</p>
        <ul class="btn-container" style="list-style-type:none">
          <li @click="onClickPack($event)" data-size="10">
            <p>1</p>
            <span>(2-3 KG)</span>
          </li>
          <li @click="onClickPack($event)" data-size="20" >
            <p>2</p>
            <span>(3-4 KG)</span>
          </li>
          <li @click="onClickPack($event)" data-size="30">
            <p>3</p>
            <span>(4-7 KG)</span>
          </li>
          <li @click="onClickPack($event)" data-size="40">
            <p>4</p>
            <span>(7-10 KG)</span>
          </li>
          <li @click="onClickPack($event)" data-size="50">
            <p>5</p>
            <span>(10-12 KG)</span>
          </li>
        </ul>
      </div>
    </div>
    <div class="test-pack-info">
      <h2>Contains Your Test Package</h2>
      <div class="columns">
        <!-- <div class="row"> -->
        <div class="column is-half">
          <div class="small-3 trial-contains-img text-center" id="diaper-design-img">
            <img
              width="25%"
              v-bind:src="require(`@/${imgDir}/lillydoo-little-blowballs-design-preview-tp.jpg`)"
            >
          </div>

          <div class="trial-info">
            <h4>10 Lillydoo diapers</h4>
            <ul>
              <li>
                <font style="vertical-align: inherit;">
                  <font
                    style="vertical-align: inherit;"
                  >0% perfumes &amp; lotions, 100% LILLYDOO protection</font>
                </font>
              </li>
              <li>
                <font style="vertical-align: inherit;">
                  <font style="vertical-align: inherit;">Extra soft and with an ideal fit</font>
                </font>
              </li>
            </ul>
          </div>
        </div>
        <div class="column is-half">
          <div class="small-3 trial-contains-img text-center">
            <img width="25%" v-bind:src="require(`@/${imgDir}/${selectedTestPack.images.wipes}`)">
          </div>
          <div class="water-wipes" v-if="showWaterPipes">
            <h4>
              <font style="vertical-align: inherit;">
                <font style="vertical-align: inherit;">15 wet wipes with 99% water</font>
              </font>
            </h4>
            <ul>
              <li>
                <font style="vertical-align: inherit;">
                  <font style="vertical-align: inherit;">0% perfumes &amp; PEGs, 100% biodegradable</font>
                </font>
              </li>
              <li>
                <font style="vertical-align: inherit;">
                  <font
                    style="vertical-align: inherit;"
                  >Naturally pure, extra mild, alternative to "water &amp; cotton"</font>
                </font>
              </li>
            </ul>
          </div>
          <div class="sensitive-wipes" v-if="!showWaterPipes">
            <h4>
              <font style="vertical-align: inherit;">
                <font style="vertical-align: inherit;">15 sensitive wet wipes</font>
              </font>
            </h4>
            <ul>
              <li>
                <font style="vertical-align: inherit;">
                  <font style="vertical-align: inherit;">0% perfumes &amp; PEGs, 100% biodegradable</font>
                </font>
              </li>
              <li>
                <font style="vertical-align: inherit;">
                  <font style="vertical-align: inherit;">Extra thick and compostable cloth</font>
                </font>
              </li>
            </ul>
          </div>
        </div>
        <!-- </div> -->
      </div>
    </div>
  </div>
</template>

<script>
import mockData from "./../data";
export default {
  name: "TestPack",
  props: {
    msg: String
  },
  methods: {
    onClickPack: function(event) {
      const size = event.target.getAttribute('data-size');
      // Selected Test pack
      this.selectedTestPack = mockData.find(d => d.size === size);
      // Show/Hide Test wipe content
      this.showWaterPipes = !this.showWaterPipes;
    }
  },
  data() {
    return {
      selectedTestPack: mockData[0],
      showWaterPipes: true,
      imgDir: "assets/images"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "./../styles/variables.scss";
.grid {
  display: -ms-grid;
  display: grid;
  // grid-template-columns: 25%;
  grid-template-rows: 30vw;
  grid-row-gap: 10em;
}

.test-pack {
  display: -ms-grid;
  display: grid;
  grid-template-columns: 40% 60%;
}

.test-pack > div {
  margin-right: 10%;
}

.test-packages > ul > li {
  border: 1px solid #7c7c7c;
  text-align: center;
  width: 30%;
  padding: 7px 5px 2px;
  color: #7c7c7c;
  margin-right: 10px;
}

.test-pack-info-container {
  display: -ms-grid;
  display: grid;
  grid-template-columns: 50% 50%;
  // grid-column-gap: 20em;
}

.text-center {
  text-align: center !important;
}
.active {
  background-color: #00afab;
  border-color: #00afab;
  color: #fff;
}

.hover {
  background-color: #00afab;
  border-color: #00afab;
  color: #fff;
}

// Media queries
/*
  ##Device = Desktops
  ##Screen = 1281px to higher resolution desktops
*/

@media (min-width: $breakpoint-bigDesktop) {
  //CSS
}

/*
  ##Device = Laptops, Desktops
  ##Screen = B/w 1025px to 1280px
*/

@media (min-width: $breakpoint-laptopMinWidth) and (max-width: $breakpoint-laptopMaxWidth) {
  //CSS
}

/*
  ##Device = Tablets, Ipads (portrait)
  ##Screen = B/w 768px to 1024px
*/

@media (min-width: $breakpoint-tabletMinWidth) and (max-width: $breakpoint-tabletMaxWidth) {
  //CSS
}

/*
  ##Device = Tablets, Ipads (landscape)
  ##Screen = B/w 768px to 1024px
*/

@media (min-width: $breakpoint-tabletMinWidth) and (max-width: $breakpoint-tabletMaxWidth) and (orientation: landscape) {
  //CSS
}

/*
  ##Device = Low Resolution Tablets, Mobiles (Landscape)
  ##Screen = B/w 481px to 767px
*/

@media (min-width: $breakpoint-mobileMinWidth) and (max-width: $breakpoint-mobileMaxWidth) {
  //CSS
}

/*
  ##Device = Most of the Smartphones Mobiles (Portrait)
  ##Screen = B/w 320px to 479px
*/

@media (min-width: $breakpoint-smallMobileMinWidth) and (max-width: $breakpoint-smallMobileMinWidth) {
  //CSS
}
</style>
