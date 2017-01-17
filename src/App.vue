<template>
<div id="app" class="card">
  <header class="card-header">
     <p class="card-header-title">
       {{ msg }}
     </p>
   </header>
    <main :class='mainClass'>
        <bulb type='incandescent' :klass='inc' :wattage='inc_wattage' :tcost='inc_tcost'></bulb>
        <bulb type='halogen' :klass='hal' :wattage='hal_wattage' :tcost='hal_tcost'></bulb>
        <bulb type='cfl' :klass='cfl' :wattage='cfl_wattage' :tcost='cfl_tcost'></bulb>
        <bulb type='led' :klass='led' :wattage='led_wattage' :tcost='led_tcost'></bulb>

    </main>
    <form>
        <div>
            <h4>Lumens</h4>
            <label>Brightness <br>of bulb</label>


            <p class="control">
                <span class="select">
                  <select v-model.number='current_lumens'>
                    <option v-for="option in lumen_options"
                            :value="option.val">
                        {{ option.val }}
                    </option>
                  </select>
                </span>
            </p>
        </div>
        <div>
            <h4>kWh</h4>
            <label>Kilowatt <br>-hours cost</label>
            <p class="control">
                <input class="input" type="number" v-model.number="current_cost" placeholder="current_cost">cents
            </p>
        </div>

        <div>
            <h4>Hours</h4>
            <label>Usage <br>per day</label>
            <p class="control">
                <input class="input" type="number" v-model.number="current_hours" placeholder="current_cost">
            </p>
        </div>
    </form>


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

            msg: 'Light Bulb Wattage Calculator App',
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
#app {
    margin: 0;
    padding: 40;
    font-size: 16px;
    /*font-family: 'Open Sans', sans-serif;
    font-weight: 300;
    line-height: 24px;*/
    max-width: 800px;
    background: black;
    color: white;
}

#app form input[type=number] {
    width: 5em;
    text-align: left;
    font-size: 1em;
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

form {
    display: flex;
    justify-content: space-around;
}
form select {
    font-size: 1em;
    padding: 3px 30px 3px 5px;

}

p+p::before {
    content: "$";
}

</style>
