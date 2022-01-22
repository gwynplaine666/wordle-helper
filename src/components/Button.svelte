<script>
    export let onClick;
</script>

<button on:click={onClick}><slot/></button>

<style>
    button {
        background: #FF4742;
        border: 1px solid #FF4742;
        border-radius: 6px;
        box-shadow: rgba(0, 0, 0, 0.1) 1px 2px 4px;
        box-sizing: border-box;
        color: black;
        cursor: pointer;
        display: inline-block;
        font-family: nunito, roboto, proxima-nova, "proxima nova", sans-serif;
        font-size: 16px;
        font-weight: 800;
        line-height: 16px;
        min-height: 40px;
        outline: 0;
        padding: 12px 14px;
        text-align: center;
        text-rendering: geometricprecision;
        text-transform: none;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        vertical-align: middle;
        transition: 0.3s;
    }
    button:hover,
    button:active {
        color: white;
    }

    button:active {
        opacity: .5;
    }
</style>