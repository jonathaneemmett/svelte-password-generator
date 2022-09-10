<script>
    import { createEventDispatcher } from "svelte";
    import CopyIcon from "./icons/CopyIcon.svelte";
    import RecycleIcon from "./icons/RecycleIcon.svelte";

    let dispatch = createEventDispatcher();

    export let text = "Sugessted Password";
    export let charlen = 16;

    let suggestedPassword = "";
    let isCopied = false;

    function copy() {
        let copiedAlert = document.getElementById("copied-alert");
        navigator.clipboard.writeText(suggestedPassword);
        copiedAlert.style.display = "block";
        console.log(suggestedPassword);
        dispatch('generatedPassword', suggestedPassword);
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

    $: isCopied && setTimeout(() => {
        let copiedAlert = document.getElementById("copied-alert");
        copiedAlert.style.display = "none";
        isCopied = false;
    }, 4000);

</script>

<div>
    <div class="gpHeader">
        <h5>{text}</h5>
        <span id="copied-alert" class="gpCopiedAlert">Copied</span>
    </div>
    <div class="gpContainer">
        <div on:click|preventDefault={() => generatePassword()}><RecycleIcon /></div>
        <div>{suggestedPassword}</div>
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
        display: grid;
        grid-template-columns: 1fr 8fr 1fr;
        margin: 5px 0 15px 0;
        border: 1px solid #ccc;
        padding: 1rem;
        border-radius: 5px;
    }

    .gpContainer div {
        display: flex;
        justify-content: center;
        align-items: center;
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