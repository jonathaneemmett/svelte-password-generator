<script>
    import { createEventDispatcher } from "svelte";
    import CopyIcon from "./icons/CopyIcon.svelte";

    let dispatch = createEventDispatcher();

    export let generatedPassword = "";
    export let charlen = 16;

    let suggestedPassword = "";
    let isCopied = false;

    function copy() {
        let copiedAlert = document.getElementById("copied-alert");
        navigator.clipboard.writeText(generatedPassword);
        copiedAlert.style.display = "block";
        generatedPassword === suggestedPassword;
        dispatch("copied");
        isCopied = true;
    }

    function generatePassword() {
        const length = charlen;
        const charset = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$';
        let retVal = "";
        for (let i = 0, n = charset.length; i < length; ++i) {
            retVal += charset.charAt(Math.floor(Math.random() * n));
        }
        suggestedPassword = retVal;
    }

    generatePassword();

    $: suggestedPassword && console.log(suggestedPassword);

    $: isCopied && setTimeout(() => {
        let copiedAlert = document.getElementById("copied-alert");
        copiedAlert.style.display = "none";
        isCopied = false;
    }, 4000);

</script>

<div>
    <div class="gpHeader">
        <h5>Suggested Password</h5>
        <span id="copied-alert" class="gpCopiedAlert">Copied</span>
    </div>
    <div class="gpContainer">
        <p>{suggestedPassword}</p>
        <div on:click|preventDefault={() => copy()}><CopyIcon /></div>
    </div>
</div>

<style>
    .gpHeader {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .gpHeader h5 {
        margin: 0 0 5px 0; 
        padding: 5px;
    }
    .gpContainer {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin: 5px 0 15px 0;
        border: 1px solid #ccc;
        padding: 1rem;
        border-radius: 5px;
    }

    .gpCopiedAlert {
        display: none;
        width: 60px;
        background: #ccc;
        
        font-size: 12px; 
        text-align: center;  
        padding: 5px; 
        border-radius: 10px; 
    }
</style>