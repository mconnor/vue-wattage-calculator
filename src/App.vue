<template>
<div id="app" class="card">
    <header class="card-header">
        <p class="card-header-title">
            {{ msg }}
        </p>
    </header>
    <div class="card-content">
        <main :class='mainClass'>
            <bulb type='incandescent' :klass='inc' :wattage='inc_wattage' :tcost='inc_tcost'></bulb>
            <bulb type='halogen' :klass='hal' :wattage='hal_wattage' :tcost='hal_tcost'></bulb>
            <bulb type='cfl' :klass='cfl' :wattage='cfl_wattage' :tcost='cfl_tcost'></bulb>
            <bulb type='led' :klass='led' :wattage='led_wattage' :tcost='led_tcost'></bulb>

        </main>
        <form>
            <div>
                <h4>Lumens</h4>
                <p>Brightness <br>of bulb</p>
                <!-- <span class="control"> -->
                <p class="select control">
                    <select v-model.number='current_lumens'>
                      <option v-for="option in lumen_options"
                              :value="option.val">
                          {{ option.val }}
                      </option>
                  </select>
                </p>
                <!-- </span -->
            </div>
            <div>
                <h4>kWh</h4>
                <p>Kilowatt <br>-hours cost</p>
                <p class="control">
                    <input class="input" type="number" v-model.number="current_cost" placeholder="current_cost">cents
                </p>
            </div>

            <div>
                <h4>Hours</h4>
                <p>Usage <br>per day</p>
                <p class="control">
                    <input class="input" type="number" v-model.number="current_hours" placeholder="current_cost">
                </p>
            </div>
        </form>
    </div>
    <footer class="card-footer">

        <!-- <a class="card-footer-item">Save</a>
           <a class="card-footer-item">Edit</a>
           <a class="card-footer-item">Delete</a>
          -->
        <p class="card-footer-item">Made with <a href='https://vuejs.org/'>Vue.js</a></p>

    </footer>


</div>
</template>

<script>
import Bulb from './components/Bulb.vue'

export default {
    name: 'app',
    components: {
        Bulb
    },
    data() {
        return {
            total_days: 365,

            inc_conv: 0.0625,
            hal_conv: 0.045,
            cfl_conv: 0.0146,
            led_conv: 0.0125,

            msg: 'Light Bulb Wattage Calculator App. Made with Vue.js',
            inc: 'bg-inc',
            hal: 'bg-hal',
            cfl: 'bg-cfl',
            led: 'bg-led',
            current_cost: 21,
            current_hours: 10,
            mainClass: 'my-main',
            lumen_options: [{
                val: 375
            }, {
                val: 600
            }, {
                val: 900
            }, {
                val: 1125
            }, {
                val: 1600
            }],
            current_lumens: 375

        }
    },


    computed: {
        // wattage(conv) {
        //   return (this.current_lumens * conv).toFixed(2);
        // },


        inc_wattage() {
            return (this.current_lumens * this.inc_conv).toFixed(2);
        },
        hal_wattage() {
            return (this.current_lumens * this.hal_conv).toFixed(2);
        },
        cfl_wattage() {
            return (this.current_lumens * this.cfl_conv).toFixed(2);
        },
        led_wattage() {
            return (this.current_lumens * this.led_conv).toFixed(2);
        },


        inc_tcost() {
            //var inc_wattage = (this.current_lumens * this.inc_conv).toFixed(2);
            //var inc_wattage = wattage(this.inc_conv);
            return ((this.inc_wattage * this.total_hours * this.cost) / 1000).toFixed(2);
        },
        hal_tcost() {
            var hal_wattage = (this.current_lumens * this.hal_conv).toFixed(2);
            return ((this.hal_wattage * this.total_hours * this.cost) / 1000).toFixed(2);
        },
        cfl_tcost() {
            var cfl_wattage = (this.current_lumens * this.cfl_conv).toFixed(2);
            return ((this.cfl_wattage * this.total_hours * this.cost) / 1000).toFixed(2);
        },
        led_tcost() {
            var led_wattage = (this.current_lumens * this.led_conv).toFixed(2);
            return ((this.led_wattage * this.total_hours * this.cost) / 1000).toFixed(2);
        },



        total_hours() {
            return this.total_days * this.current_hours;
        },
        cost() {
            return this.current_cost / 100;
        }
    }
}
</script>

<style>
@import url("../node_modules/bulma/css/bulma.css");
@import url(https://fonts.googleapis.com/css?family=Open+Sans:300,700|Open+Sans+Condensed:700);
#app {
    margin: 0;
    padding: 40;
    font-size: 16px;
    font-weight: 300;
    /*font-family: 'Open Sans', sans-serif;


    max-width: 800px;*/
    background: black;
    color: white;
}
#app .card-header-title{
  color: #fff
}
#app form input[type=number] {
    width: 5em;
    text-align: center;
    font-size: 1em;
    margin-right: 1em;
}

.control {
    margin-top: 6px;
    text-align: center;
}

.my-main {
    background: brown;
    display: flex;
    justify-content: space-around;
}

.bg-inc,
.bg-cfl,
.bg-hal,
.bg-led {
    width: 25%;
}

.bg-inc {
    background-color: red;
    background-image: url(./assets/bulb_inc.svg);
}

.bg-cfl {
    background-color: orange;
    background-image: url(./assets/bulb_cfl.svg);
}

.bg-hal {
    background-color: green;
    background-image: url(./assets/bulb_hal.svg);
}

.bg-led {
    background-color: blue;
    background-image: url(./assets/bulb_led.svg);
}

#app form {
    display: flex;
    justify-content: space-around;
}

#app form select {
    font-size: 1em;
    /*-webkit-appearance: none;
-moz-appearance: none;
appearance: none;
    background: #fff url(./assets/icons_arrows.svg) no-repeat right 6px;
  background-size: 30px 20px;*/
    padding: 3px 30px 3px 5px;
}

#app form h4 {
    color: #aaa;
    margin: 0 0 -5px 0;
    font-size: 1.5em;
    font-weight: 300;
}

#app form p {
    font-size: .8em;
    line-height: 14px;
}

#app form br {
    display: none;
}

#app form>div {
    width: 33%;
    /*float: left;*/
    text-align: center;
    color: white;
    /*padding: 10px 0 5px 0;*/
}

form::after {
    content: "";
    display: block;
    clear: both;
}

@media screen and (max-width: 500px) {
    form br {
        display: inline;
    }
}
</style>
