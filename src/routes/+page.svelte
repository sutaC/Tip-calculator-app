<script>

    let bill;
    let people;
    let tip;
    let customTip;
    

    let tipAmmount;
    $: { // Calculate tipAmmount of tip
        if(tip === "custom") {
            tipAmmount = Math.round( (((bill * (customTip / 100)) / people)  * 100)) / 100
        } else {
            tipAmmount = Math.round( (((bill * (tip / 100)) / people)  * 100)) / 100
        }
    }
    
    $: totalAmmount = Math.round(  (bill / people + tipAmmount )  * 100) /100 // Calculate tipAmmount of tip per person
    
    
    let invalidFiles = [];
    let valid = true;
    $: { // Validate data
        
        valid = true
        invalidFiles = []


        // Validate bill tipAmmount 
        if(bill > 1000000){ // Is less than or equal to 1000000
            valid = false
            invalidFiles = [...invalidFiles, {file: 'bill', message: 'Is too large'}]
        } else if (bill < 0.01) { // Is greater than or equal to 0.01
            valid = false
            invalidFiles = [...invalidFiles, {file: 'bill', message: 'Is too small'}]
        }


        // Validate the number of people
        if (totalAmmount === 0 || people > 1000000) { // Is less than or equal to 1000000 and is totalAmmount tipAmmount grater than 0
            valid = false
            invalidFiles = [...invalidFiles, {file: 'people', message: 'Is too large'}]
        } 
        else if (people < 1) { // Is greater than or equal to 1
            valid = false
            invalidFiles = [...invalidFiles, {file: 'people', message: 'Is too small'}]
        }


        // Validate tip
        if (tip === 'custom'){ // Custom tip

            if(customTip > 100){ // Is less than or equal to 100
                valid = false
                invalidFiles = [...invalidFiles, {file: 'tip', message: 'Is too large'}]
            } else if (customTip < 0.01) { // Is greater than or equal to 0.01
                valid = false
                invalidFiles = [...invalidFiles, {file: 'tip', message: 'Is too small'}]
            }

        }


        // Validate outpt
        if(isNaN(tipAmmount) || isNaN(totalAmmount)){
            valid = false
        }

    }

    const handleReset = () => {
        bill = undefined;
        people = undefined;
        tip = undefined;
        customTip = undefined;
    }

</script>
<!-- ---  -->

<header>
    <img src="/logo.svg" alt="logo">
</header>

<main>

    <section>
        <div class="wrapper">
            <h1>Bill</h1>
            {#each invalidFiles.filter(e => e.file === 'bill') as err}
                <p class="error-message">
                    {err.message}
                </p>
            {/each}
        </div>
        <div 
            class="input-field"
            class:error-field={invalidFiles.some(e => e.file === 'bill')}
        >
            <img src="/icon-dollar.svg" alt="Icon dollar">
            <input type="number" name='bill' placeholder="0" bind:value={bill} min="0.01" max="1000000">
        </div>
    </section>


    <section>
        <div class="wrapper">
            <h1>Select Tip %</h1>
            {#each invalidFiles.filter(e => e.file === 'tip') as err}
                <p class="error-message">
                    {err.message}
                </p>
            {/each}
        </div>
        <div class="select-field">

            <input type="radio" name="tip" id="tip1" value="5" bind:group={tip}>
            <label for="tip1" class="select-item">5%</label>

            <input type="radio" name="tip" id="tip2" value="10" bind:group={tip}>
            <label for="tip2" class="select-item">10%</label>

            <input type="radio" name="tip" id="tip3" value="15" bind:group={tip}>
            <label for="tip3" class="select-item">15%</label>

            <input type="radio" name="tip" id="tip4" value="25" bind:group={tip}>
            <label for="tip4" class="select-item">25%</label>

            <input type="radio" name="tip" id="tip5" value="50" bind:group={tip}>
            <label for="tip5" class="select-item">50%</label>

            <input type="radio" name="tip" id="tip6" value="custom" bind:group={tip}>
            <label for="tip6" class="select-item">
                <input 
                    type="number" 
                    placeholder="Custom" 
                    min="0.01" 
                    max="100" 
                    bind:value={customTip} 
                    class:error-field={invalidFiles.some(e => e.file === 'tip')}
                    on:click={() => tip = 'custom'}
                >
            </label>

        </div>
    </section>

    
    <section>
        <div class="wrapper">
            <h1>Number of People</h1>
            {#each invalidFiles.filter(e => e.file === 'people') as err}
                <p class="error-message">
                    {err.message}
                </p>
            {/each}
        </div>
        <div 
            class="input-field"
            class:error-field={invalidFiles.some(e => e.file === 'people')}
        >
            <img src="/icon-person.svg" alt="Icon person">
            <input 
                type="number" 
                name='people' 
                placeholder="0" 
                min="1" 
                max="1000000"
                bind:value={people} 
            >
        </div>
    </section>
    
    <div class="summary">

        <div>
            <div class="wrapper">
                <div class="summary-block">
                    <h2>Tip Amount</h2>
                    <p>/ person</p>
                </div>
                <p class="tipAmmount">
                    $
                    {#if valid}
                        {tipAmmount}
                    {:else if invalidFiles.length > 0}
                        -.--
                    {:else}
                        0.00
                    {/if}
                </p>
            </div>
            <div class="wrapper">
                <div class="summary-block">
                    <h2>Total</h2>
                    <p>/ person</p>
                </div>
                <p class="tipAmmount">
                    $
                    {#if valid}
                        {totalAmmount}
                    {:else if invalidFiles.length > 0}
                        -.--
                    {:else}
                        0.00    
                    {/if}
                </p>
            </div>
        </div>
        
        <button 
            disabled={!bill && !people && !tip && !customTip}
            on:click={handleReset}
        >
            RESET
        </button>

    </div>

    
</main>


<!-- ---  -->
<style>

    @import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@700&display=swap');

    :root {

        /* # Typography # */
        --ff-space-mono: 'Space Mono', monospace;
        --fz--regular: 24px;
        --fw-700-regular: 700;

        /* # Colors #  */
        /* Primary */
        --clr-strong-cyan: hsl(172, 67%, 45%);
        /* Neutral */
        --clr-very-dark-cyan: hsl(183, 100%, 15%);
        --clr-dark-grayish-cyan: hsl(186, 14%, 43%);
        --clr-grayish-cyan: hsl(184, 14%, 56%);
        --clr-light-grayish-cyan: hsl(185, 41%, 84%);
        --clr-very-light-grayish-cyan: hsl(189, 41%, 97%);
        --clr-white: hsl(0, 0%, 100%);

    }

    * {
        font-family: var(--ff-space-mono);
        font-size: var(--fz--24px-regular);
    }

    /* # Main styles # */

    :global(body) {
        display: flex;
        flex-direction: column;
        justify-content: center;

        box-sizing: border-box;
        min-height: 100vh;

        margin: 0;
        padding: 0;

        background-color: var(--clr-light-grayish-cyan);
    }


    header {

        display: flex;
        justify-content: center;
        align-items: center;

        max-width: 100%;
        min-height: 8rem;


    }

    main {
        box-sizing: border-box;
        flex: 1;

        max-width: 100%;

        padding: 1rem;

        border-radius: 1rem 1rem 0 0;

        background-color: var(--clr-white);
    }
    main > * {
        max-width: 100%;
        margin-bottom: 2rem;
    }


    section h1 {
        font-size: 0.9rem;
        color: var(--clr-grayish-cyan);
    }


    .input-field {
        box-sizing: border-box;

        padding: 0.5rem;

        border: 2px solid transparent;
        border-radius: 0.5rem;
        
        background-color: var(--clr-very-light-grayish-cyan);
    }
    .input-field:focus-within:not(.error-field) {
        border: 2px solid var(--clr-strong-cyan);
    }
    .input-field input {
        width: 90%;
        
        padding: 0;
        
        border: none;
        outline: none;
        
        text-align: right;
        
        background-color: var(--clr-very-light-grayish-cyan);
    }
    
    
    
    .select-field {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        grid-auto-rows: 1fr;
        
        width: 100%;
    }
    
    .select-field input[type="radio"] {
        display: none;
    }
    
    .select-item {
        display: flex;
        align-items: center;
        justify-content: center;
        
        box-sizing: border-box;
        margin: 0.5rem;
        
        min-height: 2.5rem;
        max-width: 7rem;

        border-radius: 0.3rem;
        
        font-size: 1.1rem;
        text-align: center;
        color: var(--clr-white);
        
        background-color: var(--clr-very-dark-cyan);
    }
    .select-item:hover:not(.select-field > input:checked + label) {
        background-color: var(--clr-light-grayish-cyan);
        color: var(--clr-very-dark-cyan);
    }
    .select-field > input:checked + label {
        background-color: var(--clr-strong-cyan);
        color: var(--clr-very-dark-cyan );
    }

    .select-item:last-of-type {
        background-color: var(--clr-very-light-grayish-cyan);
        border: 2px solid transparent;
    }
    .select-item:last-of-type > input {
        box-sizing: border-box;
        width: 100%;
        
        border: none;
        outline: none;
        
        text-align: right;

        background-color: transparent;
    }
    .select-field > input:last-of-type:checked + label {
        background-color: var(--clr-very-light-grayish-cyan);
        border: 2px solid var(--clr-strong-cyan);

    }
    

    
    
    .summary {
        box-sizing: border-box;
        padding: 1rem;

        border-radius: 1rem;

        background-color: var(--clr-very-dark-cyan);
    }
    .summary * {
        margin: 0;
    }
    .summary > * {
        margin: 1rem 0;
    }

    .summary > div > * {
        margin: 1rem 0;
    }

    .summary button {
        box-sizing: border-box;
        width: 100%;

        padding: 0.5rem 0;

        border: none;
        border-radius: 0.5rem;

        background-color: var(--clr-strong-cyan);

        color: var(--clr-very-dark-cyan);
        text-transform: capitalize;
    }
    .summary button:active {
        background-color: var(--clr-light-grayish-cyan);
    }
    .summary button:disabled {
        opacity: 0.5;
    }

    .summary-block > h2 {
        font-size: 0.8rem;
        color: var(--clr-white);
    }
    .summary-block > p {
        font-size: 0.7rem;
        color: var(--clr-grayish-cyan);
    }

    .tipAmmount {
        font-size: 2.5em;
        color: var(--clr-strong-cyan);
    }



    .wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .error-message {
        font-size: 0.8rem;
        color: red;
    }
    .error-field {
        border: 2px solid red;
    }


    /* # Desktp styles # */

    @media (min-width: 550px) {

        :global(body) {
            align-items: center;
        }

        main {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            grid-template-rows: repeat(3, minmax(0, 1fr));
            gap: 1rem;

            border-radius: 1rem;

            max-height: 29rem;
        }
        main > * {
            margin: 0;
        }

        .summary {
            display: flex;
            flex-direction: column;
            justify-content: space-between;

            grid-column: 2;
            grid-row: 1/4;

        }

        .select-field {
            grid-template-columns: repeat(3, minmax(0, 1fr));
        }

    }

</style>