<script>
  import { onMount } from "svelte";

  let uppercaseEachWord = false;
  // TODO: Reactive value, aber ohne dass ich alle ändernden Parameter reinreichen muss.
  // Oder will ich das, weil ich strikt funktional programmieren will?
  // TODO: Das Passwort soll bei manchen Parametern geändert werden (Länge, Zahl),
  // aber nicht bei allen (Uppercase, Trennzeichen)
  $: password = calculatePassword(uppercaseEachWord);
  
  let allWords;

  async function loadAllWords() {
    if ( allWords ) {
      return allWords;
    }
    // TODO: is this loaded again after every nav change?
    const response = await fetch(`/words_comma.txt`)
    const responseString = await response.text()
    // TODO: what is fastest? JSON array inside the file? splitting here?
    allWords = responseString.split(',')
  }

  // https://stackoverflow.com/questions/19269545/how-to-get-a-number-of-random-elements-from-an-array
  function getRandomWordsFromAllWords(n, uppercaseEachWord) {
    var result = new Array(n),
      len = allWords.length,
      taken = new Array(len),
      currentWord;
    if (n > len)
      throw new RangeError("getRandom: more elements taken than available");
    while (n--) {
      // TODO: die taken Sache kann ich doch löschen oder reverten?
      var x = Math.floor(Math.random() * len);
      currentWord = allWords[x in taken ? taken[x] : x];
      if(uppercaseEachWord) {
        currentWord = currentWord.charAt(0).toUpperCase() + currentWord.slice(1)
      }
      result[n] = currentWord;
      //console.log('result', result);
      taken[x] = --len in taken ? taken[len] : len;
      //console.log('taken', taken);
    }
    return result;
  }

  async function calculatePassword(uppercaseEachWord) {
      await loadAllWords();
      // TODO: input elements for word length, uppercase, ...
      let words = getRandomWordsFromAllWords(4, uppercaseEachWord)
      words.push(Math.ceil(Math.random()*10))
      password = words.join('-')
  }

  onMount(async () => {
    await calculatePassword(uppercaseEachWord)
  });
</script>

<div>
  <h1>Correct Horse Battery Staple</h1>

  <!-- {!character ? 'Loading ...' : character.name} -->
  {#if password}
    <p>{ password }</p>
  {:else}
    <p>loading...</p>
  {/if}

  <label>
    <input type=checkbox bind:checked={uppercaseEachWord}>
    Begin each word with an uppercase character.
  </label>
  <!-- TODO: BIG REPEAT BUTTON like in Dice-->
</div>
