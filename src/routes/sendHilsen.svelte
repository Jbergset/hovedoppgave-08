<svelte:head>
    <title>Send en hilsen</title>
</svelte:head>

<script>
    import {onMount} from "svelte"

    let db
    let hilsenTittel
    let textID
    let hilsen
    let hilsener = []

    let tittel
    let text

    onMount(
        async () => {
            db = firebase.firestore()
            hilsen = db.collection("hilsen")
            hilsen.onSnapshot(snap => {
                hilsener = snap.docs
            })
        }
    )

    const regHilsen = () => {
        hilsen
            .doc()
            .set({
                tittel: hilsenTittel,
                text: textID,
                tid: firebase.firestore.FieldValue.serverTimestamp()
        })
            tittel = ""
            text = ""

    }
</script>
<h1>Her kan du sende din hilsen</h1>

<form on:submit|preventDefault={regHilsen}>
    <input bind:value={hilsenTittel} id="textTittel"placeholder="Tittel på din hilsning" required>
    <br> 
    <br>
    <input type="text" id="textHilsen" bind:value={textID} placeholder="Skriv noe hyggelig her" required>
    <button>Send din hilsen</button>
</form>

<style>
    #textHilsen {
        height: 220px;
        width: 800px;
        border-radius: 5px;
    }
    #textTittel {
        height: 50px;
        width: 350px;
        border-radius: 5px;
        font-size: 25px;
    }
</style>