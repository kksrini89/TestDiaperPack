<template>
  <div>
    <nav class="navbar is-fixed-top main-navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="#">
          <h2>LILLYDOO</h2>
        </a>
      </div>
    </nav>
    <div class="main container">
      <div class="test-pack columns is-mobile">
        <div class="diaper-images column is-5">
          <img v-bind:src="require(`@/${imgDir}/${selectedTestPack.images.trial_pack}`)">
        </div>
        <div class="test-packages column is-6">
          <section class="hero">
            <div class="hero-body">
              <h1 class="title">Our Free Test Package</h1>
              <h2 class="subtitle">choose your size</h2>
            </div>
          </section>
          <!-- <h2>Our Free Test Package</h2>
          <p style="text-transform: uppercase;">choose your size</p>-->
          <ul class="btn-container">
            <li
              @click="onClickPack($event)"
              data-size="10"
              :class="{active: isActiveSize, button: true}"
            >
              <p v-on:click.stop>1</p>
              <span v-on:click.stop>(2-3 KG)</span>
            </li>
            <li @click="onClickPack($event)" data-size="20" class="button">
              <p v-on:click.stop>2</p>
              <span v-on:click.stop>(3-4 KG)</span>
            </li>
            <li @click="onClickPack($event)" data-size="30" class="button">
              <p v-on:click.stop>3</p>
              <span v-on:click.stop>(4-7 KG)</span>
            </li>
            <li @click="onClickPack($event)" data-size="40" class="button">
              <p v-on:click.stop>4</p>
              <span v-on:click.stop>(7-10 KG)</span>
            </li>
            <li @click="onClickPack($event)" data-size="50" class="button">
              <p v-on:click.stop>5</p>
              <span v-on:click.stop>(10-12 KG)</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="test-pack-info">
        <h2 class="title">Contains Your Test Package</h2>
        <div class="columns">
          <!-- <div class="row"> -->
          <div class="column is-half">
            <div class="columns">
              <div class="column is-4 text-center" id="diaper-design-img">
                <img
                  v-bind:src="require(`@/${imgDir}/lillydoo-little-blowballs-design-preview-tp.jpg`)"
                >
              </div>

              <div class="column is-6 trial-info">
                <h4>10 Lillydoo diapers</h4>
                <ul>
                  <li>0% perfumes &amp; lotions, 100% LILLYDOO protection</li>
                  <li>Extra soft and with an ideal fit</li>
                </ul>
              </div>
            </div>
          </div>
          <div class="column is-half">
            <div class="columns">
              <div class="column is-4 text-center">
                <img v-bind:src="require(`@/${imgDir}/${selectedTestPack.images.wipes}`)">
              </div>
              <div class="column is-6 water-wipes" v-if="showWaterPipes">
                <h4>15 wet wipes with 99% water</h4>
                <ul>
                  <li>0% perfumes &amp; PEGs, 100% biodegradable</li>
                  <li>Naturally pure, extra mild, alternative to "water &amp; cotton"</li>
                </ul>
              </div>
              <div class="column is-6 sensitive-wipes" v-if="!showWaterPipes">
                <h4>15 sensitive wet wipes</h4>
                <ul>
                  <li>0% perfumes &amp; PEGs, 100% biodegradable</li>
                  <li>Extra thick and compostable cloth</li>
                </ul>
              </div>
            </div>
          </div>
          <!-- </div> -->
        </div>
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
      // Stopping event bublling to child element
      event.stopPropagation();

      // Removing active class from any other element if already exists
      let nodes = document.querySelectorAll("li.active");
      // nodes[0].classList.remove('active');
      Array.from(nodes).map(node => node.classList.remove("active"));

      // Adding active class to currently clicked element
      let classNames = event.target.classList;
      classNames.add("active");

      const size = event.target.getAttribute("data-size");
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
      isActiveSize: true,
      isHoveringOnSize: false,
      imgDir: "assets/images"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "./../styles/variables.scss";
@import "../../node_modules/bulma/bulma.sass";
@mixin active {
  background-color: #3273dc;
  // border-color: #00afab;
  border-color: transparent;
  color: #fff !important;
}

.active {
  @include active;
}
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

.test-packages > ul.btn-container {
  list-style-type: none;
  padding-top: 5%;
  & > li {
    float: left;
    border: 1px solid #7c7c7c;
    text-align: center;
    width: 15%;
    padding: 7px 5px 2px;
    color: #7c7c7c;
    margin-right: 10px;

    &:hover {
      @include active;
    }
  }
}

.test-pack-info-container {
  display: -ms-grid;
  display: grid;
  grid-template-columns: 50% 50%;
  // grid-column-gap: 20em;
}

.test-pack-info {
  & ul {
    list-style-type: circle;
    text-align: left;
    & > li {
      font-size: 14px;
    }
  }
  & h2 {
    font-size: 1.5rem !important;
  }
  & h4 {
    text-align: left;
  }
}

.text-center {
  text-align: center !important;
}

h4 {
  font-weight: 600;
  font-size: 1rem;
  line-height: 1.5;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.main-navbar {
  background-color: gainsboro;
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
  .test-packages {
    & .btn-container {
      & li {
        font-size: 8px;
      }
    }
  }
  .test-pack-info {
    & ul {
      list-style: circle;
    }
  }
}

/*
  ##Device = Most of the Smartphones Mobiles (Portrait)
  ##Screen = B/w 320px to 479px
*/

@media (min-width: $breakpoint-smallMobileMinWidth) and (max-width: $breakpoint-smallMobileMinWidth) {
  //CSS
}
</style>
