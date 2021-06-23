<script>
  import { translationsLeft } from '../store.js';

  let translations;

  translationsLeft.subscribe(val => {
    translations = val;
  });
</script>

<div>
  <p>
    In <span>nonsensikal</span>, you can translate a phrase to up to 50 different <i>WEIRD</i> languages. In order to do so, we are using an API developed by the good folks from <a href="https://funtranslations.com/api/">Fun Translations</a>. In addition to that, thanks to the peeps from <a href="https://api.adviceslip.com/">Advice Slip</a>, we provide you with random advices that you can use to test our translator!
  </p>
  <p>
    Because of the former, the translator is limited to a maximum of 5 translations per hour, which translates to (ba, dum, tss!) a maximum of 60 translates per day. We hope that you can still enjoy it, despite it's limitations! To make it easier for you, we have added a tracker of the ammount of translations performed, so you know exactly when to stop (or when it will stop working).
  </p>
  <p id="counter">Translations remaining: {translations}</p>
</div>

<style>
  div {
    margin-inline: 30px;
  }

  p {
    font-family: 'Raleway';
    font-size: 14px;
    line-height: 24px;
    margin: 0 0 24px;
    text-align: justify;
    text-justify: inter-word;
  }

  #counter {
    text-align: center;
  }

  span {
    font-family: "Poppins", sans-serif;
    font-weight: 300;
    margin: 0px 5px;
  }

  a {
    color: #2E5266;
    text-decoration: unerline;
    text-decoration-color: #F58A07;
  }

  a:visited {
    color: #2E5266;
    text-decoration: unerline;
    text-decoration-color: #F58A07;
  }
</style>