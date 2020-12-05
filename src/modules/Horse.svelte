<script>
  import { onMount } from "svelte";

  // https://stackoverflow.com/questions/19269545/how-to-get-a-number-of-random-elements-from-an-array
  function getRandom(arr, n) {
    var result = new Array(n),
      len = arr.length,
      taken = new Array(len);
    if (n > len)
      throw new RangeError("getRandom: more elements taken than available");
    while (n--) {
      var x = Math.floor(Math.random() * len);
      result[n] = arr[x in taken ? taken[x] : x];
      taken[x] = --len in taken ? taken[len] : len;
    }
    return result;
  }

  
  let password;

  onMount(async () => {
    // TODO: is this loaded again after every nav change?
    const response = await fetch(`/words_comma.txt`)
    const responseString = await response.text()
    // TODO: what is fastest? JSON array inside the file? splitting here?
    const allWords = responseString.split(',')
    
    // TODO: input elements for word length, uppercase, 
    let words = getRandom(allWords, 4)
    words.push(Math.ceil(Math.random()*10))
    password = words.join('-')
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

  <!-- TODO: BIG REPEAT BUTTON like in Dice-->
</div>
