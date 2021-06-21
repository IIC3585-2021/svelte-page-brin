<script>
  import { storedAdvice } from '../store.js';

  let advice = '';
  let disableButton = false;

  async function getAdvice() {
    const apiUrl = "https://api.adviceslip.com/advice";

    // disable the button while we request a new advice
    disableButton = true;
    const request = await fetch(apiUrl, {
      method: 'GET',
    });

    // decode the answer and set the advice
    const newAdvice = await request.json()
    advice = newAdvice.slip.advice;

    // enable the button
    disableButton = false;

    // update the advice on the store for the translator
    storedAdvice.update(() => newAdvice.slip.advice);
  }
</script>

<div id="advice-container">
  <p>
    Don't know what to translate? <br>
    Try with this random advice:
  </p>

  <button on:click={getAdvice} disabled={disableButton}> Give me an advice! </button>

  <div class="advice">
    {advice}
  </div>
</div>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700;800;900&display=swap");

  #advice-container {
    display: flex;
    flex-direction: column;
    margin: 0 auto;
  }

  .advice {
    text-align: center;
    font-size: 16pt;
    font-family: "Poppins", sans-serif;
    margin: 10px;
  }

  button {
    margin: 10px auto;
    background-color: transparent;
    padding: 10px;
    font-family: "Poppins", sans-serif;
    text-decoration: none;
    text-transform: uppercase;
    text-align: center;
    font-weight: 500;
    font-size: 11pt;
    border: 2px solid #260C1A;
    color: #260C1A;
  }

  button:disabled {
    background-color: #C8C8C8;
    color: #707070;
    border: 2px solid #707070;
  }

  p {
    text-align: center;
    font-family: 'Raleway';
    font-size: 14px;
    line-height: 24px;
  }
</style>
