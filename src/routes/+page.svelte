<script>



</script>
<!-- ---  -->

<header>
    <img src="/logo.svg" alt="logo">
</header>

<main>

    <section>
        <div class="wrapper">
            <h1>Bill</h1>
            <p class="error-message">err</p>
        </div>
        <div class="input-field">
            <img src="/icon-dollar.svg" alt="Icon dollar">
            <input type="number" name='bill' placeholder="0">
        </div>
    </section>


    <section>
        <div class="wrapper">
            <h1>Select Tip %</h1>
            <p class="error-message">err</p>
        </div>
        <div class="select-field">
            <div class="select-item"><input type="radio" name="tip" id="tip1"><label for="tip1">5%</label></div>
            <div class="select-item"><input type="radio" name="tip" id="tip2"><label for="tip2">10%</label></div>
            <div class="select-item"><input type="radio" name="tip" id="tip3" checked><label for="tip3">15%</label></div>
            <div class="select-item"><input type="radio" name="tip" id="tip4"><label for="tip4">25%</label></div>
            <div class="select-item"><input type="radio" name="tip" id="tip5"><label for="tip5">50%</label></div>
            <div class="select-item">
                <input type="radio" name="tip" id="tip6">
                <label for="tip6">
                    <input type="number" placeholder="Custom">
                </label>
            </div>
        </div>
    </section>

    
    <section>
        <div class="wrapper">
            <h1>Number of People</h1>
            <p class="error-message">err</p>
        </div>
        <div class="input-field error-field">
            <img src="/icon-person.svg" alt="Icon person">
            <input type="number" name='people' placeholder="0">
        </div>
    </section>
    
    <div class="summary">

        <div class="wrapper">
            <div class="summary-block">
                <h2>Tip Amount</h2>
                <p>/ person</p>
            </div>
            <p class="ammount">$0.00</p>
        </div>
        <div class="wrapper">
            <div class="summary-block">
                <h2>Total</h2>
                <p>/ person</p>
            </div>
            <p class="ammount">$0.00</p>
        </div>
        
        <button>RESET</button>

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
        



        font-family: var(--ff-space-mono);
        font-size: var(--fz--24px-regular);

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
        align-items: center;

        box-sizing: border-box;
        min-height: 100vh;
        width: 100vw;

        margin: 0;
        padding: 0;

        background-color: var(--clr-light-grayish-cyan);
    }


    header {

        display: flex;
        justify-content: center;
        align-items: center;

        width: 100%;
        min-height: 10rem;


    }

    main {
        box-sizing: border-box;
        width: 100%;

        padding: 10%;

        border-radius: 1rem 1rem 0 0;

        background-color: var(--clr-white);
    }
    main > * {
        max-width: 100%;
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
    .input-field:focus-within {
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


    .select-item {
        display: flex;
        align-items: center;
        justify-content: center;
        
        margin: 0.5rem;
        
        min-height: 2.5rem;
        
        font-size: 1.1rem;
        text-align: center;
        color: var(--clr-white);
        
        background-color: var(--clr-very-dark-cyan);
    }
    .select-item:hover {
        background-color: var(--clr-light-grayish-cyan);
        color: var(--clr-very-dark-cyan);
    }
    .select-item + .select-item input[type="radio"]:checked  {
        background-color: red;
    }

    
    .select-item:last-of-type {
        background-color: var(--clr-very-light-grayish-cyan);
        border: 2px solid transparent;
    }
    .select-item:last-of-type:focus-within {
        border: 2px solid var(--clr-strong-cyan);
    }
    .select-item:last-of-type > label > input {
        box-sizing: border-box;
        width: 100%;
        
        border: none;
        outline: none;
        
        text-align: right;

        background-color: transparent;
    }
    

    .select-item input[type="radio"] {
        display: none;
    }
    .select-item label {
        width: 100%;
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
    .summary-block > h2 {
        font-size: 0.8rem;
        color: var(--clr-white);
    }
    .summary-block > p {
        font-size: 0.7rem;
        color: var(--clr-grayish-cyan);
    }
    .ammount {
        font-size: 1.5rem;
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

</style>