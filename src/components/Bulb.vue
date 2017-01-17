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

font-size: 1em;
/*font-family: 'Open Sans', sans-serif;
line-height: 24px;*/
    font-weight: 300;


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



section h4 {
    font-family: 'Open Sans Condensed', sans-serif;
    font-size: .9em;
    letter-spacing: 1px;
    margin: 0 0 5px 0;
    text-transform: uppercase;
}

section p {
    margin: 0;
    font-size: 1.5em;
    font-weight: 700;
}

/*style applies to p followin another p*/
section p + p {
    font-size: 1em !important;
    font-weight: 300;
}

section p::after {
    content: 'w';
}


section p + p::after {
    content: 'per year';
    color: rgba(255, 255, 255, .5);
    padding-left: 4px;
}

section p + p::before {
    content: '$';
}


@media screen and (max-width: 500px) {
    {
        font-size: 15px;
    }

    section {
        background-size: 45px 71px;
        padding-top: 80px;
    }

    section h4 {
      font-family: 'Open Sans Condensed', sans-serif;
  font-size: .8em;
  letter-spacing: 1px;
  margin: 0 0 5px 0;
  text-transform: uppercase;
    }

    section p {
        font-size: 1.1em;
        font-size: 1.5em;
    font-weight: 700;
    }

    section p + p {
        font-size: 1em;
        font-weight: 300
    }

    section p + p::after {

        display: block;
        color: #00f;
        margin-top: -10px;
    }

}
</style>
