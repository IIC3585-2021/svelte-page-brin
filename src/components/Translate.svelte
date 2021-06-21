<script>
  import { storedAdvice, translationsLeft } from '../store.js';

  let advice;
  storedAdvice.subscribe(value => {
		advice = value;
	});

  let txt = '';
  let language = '';
  let translate = '';
  let disableButton = false;

  async function getTranslation() {
    const apiUrl = "https://api.funtranslations.com/translate/" + language + ".json?text=";
    disableButton = true;

    const res = await fetch(apiUrl + txt.split(" ").join("%20"));

    const answer = await res.json();
    disableButton = false;

    if (answer.contents) {
      translationsLeft.update(n => n - 1);
			return answer.contents.translated;
		} else {
			throw new Error("Solicitud incorrecta");
		}
  }

  let promise = "";

  function handleClick() {
		promise = getTranslation();
	}

  function copyAdvice() {
    txt = advice;
  }
</script>

<div class="container">
  <select bind:value={language} id="language"> 
    <option value="">Pick a language
    <option value="yoda">Yoda
    <option value="pirate">Pirate
    <option value="valspeak">Valspeak
    <option value="minion">Minion
    <option value="ferb-latin">Ferb-latin
    <option value="pig-latin">Pig-latin
    <option value="dothraki">Dothraki
    <option value="valyrian">Valyrian
    <option value="hodor">Hodor
    <option value="sindarin">Sindarin
    <option value="quenya">Quenya
    <option value="orcish">Orcish
    <option value="sith">Sith
    <option value="cheunh">Cheunh
    <option value="gungan">Gungan
    <option value="mandalorian">Mandalorian
    <option value="huttese">Huttese
    <option value="chef">Chef
    <option value="catalan">Catalan
    <option value="oldenglish">Oldenglish
    <option value="shakespeare">Shakespeare
    <option value="vulcan">Vulcan
    <option value="klingon">Klingon
    <option value="romulan">Romulan
    <option value="dovahzul">Dovahzul
    <option value="thuum">Thuum
    <option value="aldemirs">Aldemirs
    <option value="groot">Groot
    <option value="jive">Jive
    <option value="ebonics">Ebonics
    <option value="dolan">Dolan
    <option value="fudd">Fudd
    <option value="kraut">Kraut
    <option value="wow">Wow
    <option value="cockney">Cockney
    <option value="norfolk">Norfolk
    <option value="morse">Morse
    <option value="us2uk">US to UK
    <option value="uk2us">UK to US
    <option value="leetspeak">Leetspeak
    <option value="brooklyn">Brooklyn
    <option value="ermahgerd">Ermahgerd
    <option value="australian">Australian
    <option value="boston">Boston
    <option value="austrian">Austrian
    <option value="article_rewrite">Article rewrite
    <option value="braille">Braille
    <option value="numbers">Numbers
    <option value="emoji">Emoji
    <option value="doge">Doge
    <option value="navi">Navi
    <option value="southern-accent">Southern accent
    <option value="ubbi-dubbi">Ubbi-dubbi
    <option value="inflationary-english">Inflationary english
    <option value="george-bush-dubya">George Bush dubya
    <option value="post-modern">Post-modern
    <option value="ayleidoon">Ayleidoon
    <option value="redneck">Redneck
    <option value="roman-numerals">Roman numerals
    <option value="russian-accent">Russian accent
    <option value="english-contraction">English contraction
    <option value="irish">Irish
    <option value="british">British
    <option value="german-accent">German accent
    <option value="draconic">Draconic
  </select>
  
  <textarea bind:value={txt} id="message" cols="30" rows="7" placeholder="Input text"></textarea>
  
  <div id="buttons-container">
    <button type="button" on:click={handleClick} disabled={disableButton}>Translate</button>
    <button type="button" on:click={copyAdvice} >Copy advice</button>
  </div>
  

  <div>
    {#await promise}
      <p>...waiting</p>
    {:then number}
      <p>{number}</p>
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}
  </div>
</div>

<style>
  textarea, select {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-family: inherit;
  }

  button {
    background-color: #260C1A;
    color: white;
    padding: 14px 20px;
    margin: 8px 1rem;
    border: none;
    cursor: pointer;
    font-family: inherit;
    letter-spacing: 2px;
    font-size: 16px;
    box-shadow: 2px 2px 5px black;
    width: 10rem;
  }

  button:hover {
    background-color: #28965A;
  }

  #buttons-container {
    display: flex;
    justify-content: center;
  }

  .container {
    padding: 0px 20px;
    font-family: 'Raleway';
  }
  p {
    text-align: center;
    font-size: 16pt;
    font-family: "Poppins", sans-serif;
    margin: 10px;
  }
</style>