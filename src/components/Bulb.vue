<template>

  <section :class='klass'>
      <h4>{{type}}</h4>
      <p>{{wattage}}</p>
      <p>{{tcost}}</p>
  </section>


</template>

<script >
export default {
    name: 'bulb',
    props: {
      klass: {required: true},
      type: {required: true},
      wattage: {required: true, default: '11'},
      tcost: {required: true, default: '12'}
    },
    data() {
        return {

        }
    }
}
</script>

<style scoped>

section {


    text-align: center;

    padding-top: 110px;
    background-position: center 5px;
    background-size: 63px 100px;
    background-repeat: no-repeat;

}


/* apply rule on first descendent div */
section > div {
    padding: 5px 0;
    background-color: rgba(0, 0, 0, .15)
}



h4 {
    font-family: 'Open Sans Condensed', sans-serif;
    font-size: .8em;
    letter-spacing: 1px;
    margin: 0 0 5px 0;
    text-transform: uppercase;
}

p {
    margin: 0;
    font-size: 1.5em;
    font-weight: 700;
}

// style applies to p followin another p
p + p {
    font-size: 1em;
    font-weight: 300
}

section p::after {
    content: 'w';
}


p + p::after {
    content: 'per year';
    color: rgba(255, 255, 255, .5);
    padding-left: 4px;
}
</style>
