<script>
    import PasswordStage from './blocks/PasswordStage.svelte'

    let domain = '';
    let secret = '';

    $: password = hash(domain + secret);
  
    // https://webbjocke.com/javascript-web-encryption-and-hashing-with-the-crypto-api/
    // Returns if browser supports the crypto api
    function supportsCrypto () {
        return window.crypto && crypto.subtle && window.TextEncoder;
    }
    
    // Hash function in javascript
    async function hash (str) {
        return crypto.subtle.digest('SHA-256', new TextEncoder().encode(str));
    }
    /*
    hash('SHA-256', 'Hello').then(hashed => {
        console.log(hashed); // ArrayBuffer
        console.log(hex(hashed)); // 185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
        console.log(encode64(hashed)); // GF+NsyJx/iX1Yab8k4suJkMG7DBO2lGAB9F2SCY4GWk=
    });
    */  
    // Hex function for ArrayBuffer
    function hex (buff) {
        return [].map.call(new Uint8Array(buff), b => ('00' + b.toString(16)).slice(-2)).join('');
    }
    // Base64 encode
    function encode64 (buff) {
        return btoa(new Uint8Array(buff).reduce((s, b) => s + String.fromCharCode(b), ''));
    }

  </script>
  
  <div>
    <h1>Generate password from domain and secret</h1>
    
    <label>Domain: <input bind:value={domain}></label>
    <label>Secret: <input bind:value={secret}></label>
    
    <hr>

    {#await password then value}
        <p>the hex(value) is</p>
        <PasswordStage password={ hex(value) } />
        <p>the encode64(value) is</p>
        <PasswordStage password={ encode64(value) } />
    {/await}
    
  </div>

<!--
// TODO: Try alternatives
// - https://www.npmjs.com/package/string-hash
// - simply md5 ?
// - https://www.webbjocke.com/javascript-web-encryption-and-hashing-with-the-crypto-api/
// - https://github.com/h2non/jshashes
// - https://github.com/bitwiseshiftleft/sjcl/blob/master/sjcl.js
-->