<script>
    let height = "250px";

    let numberPerBox = 2;
    let boxCount = 4;
    let position = 0;
    let pinArr = [];
    let currentPin = "        ";
    let unlock = false;

    function setCharAt(str, index, chr) {
        if (index > str.length - 1) return str;
        return str.substring(0, index) + chr + str.substring(index + 1);
    }
    // TODO: find a way to track global keyup in svelte

    // function handleKeyup(e) {
    //     console.log(e.key);
    //      let string = String.fromCharCode(e.key);
    // }
    document.onkeyup = function (event) {
        let char = typeof event !== "undefined" ? event.keyCode : event.which;
        console.log(position);
        if (char == 8 && position >= 0) {

            if(position%2==0 && position>0){
                currentPin = setCharAt(currentPin, position-2, " ");
                currentPin = setCharAt(currentPin, position-1, " ");
                position-=2; 
                console.log("two",position);
            }
            if (position%2!=0 && position > 0) {
                currentPin = setCharAt(currentPin, position-1, " ");
                position--; 
                console.log("one",position);
            }
        } else {
            if (position < boxCount * numberPerBox) {
                let string = String.fromCharCode(char);
                if (!isNaN(parseInt(string))) {
                    console.log("currentPin:", currentPin);
                    currentPin = setCharAt(currentPin, position, string);
                    position++;
                }
            }
        }
    };
</script>

<div class="pinFlexContainer" style="height: {height}">
    <div class="numberBox flex-vertical-center">
        <input
            tabindex="-1"
            maxlength="2"
            class="text prevent-select"
            style="height: {height}"
            value={currentPin.substring(0, numberPerBox)}
        />
    </div>

    <div class="numberBox flex-vertical-center">
        <input
            tabindex="-1"
            maxlength="2"
            class="text prevent-select"
            style="height: {height}"
            value={currentPin.substring(numberPerBox, numberPerBox * 2)}
        />
    </div>

    <div class="numberBox flex-vertical-center">
        <input
            tabindex="-1"
            maxlength="2"
            class="text prevent-select"
            style="height: {height}"
            value={currentPin.substring(numberPerBox * 2, numberPerBox * 3)}
        />
    </div>

    <div class="numberBox flex-vertical-center">
        <input
            tabindex="-1"
            maxlength="2"
            class="text prevent-select"
            style="height: {height}"
            value={currentPin.substring(numberPerBox * 3, numberPerBox * 4)}
        />
    </div>
</div>

<style>
    .prevent-select {
        -webkit-user-select: none; /* Safari */
        -ms-user-select: none; /* IE 10 and IE 11 */
        user-select: none; /* Standard syntax */
    }

    ::selection {
        background: none;
    }

    @font-face {
        font-family: "Gelasio";
        font-style: normal;
        font-weight: 400;
        src: local("Gelasio Regular"), local("Gelasio-Regular"),
            url(https://fonts.gstatic.com/s/gelasio/v1/cIf9MaFfvUQxTTqS9C6hYQ.woff2)
                format("woff2");
        unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6,
            U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193,
            U+2212, U+2215, U+FEFF, U+FFFD;
    }

    .numberBox {
        border-radius: 25px;
        border: 2px solid #464745;
        font-variation-settings: "wght" 850, "wdth" 90, "opsz" 90;
        background-color: rgb(212, 212, 212);
    }

    .pinFlexContainer {
        display: flex; /* or inline-flex */
        align-items: center;
        gap: 10px;
    }

    input {
        all: unset;
        pointer-events: none;
    }
    .text {
        z-index: 2;
        width: 250px;
        /* height: var(height); */
        text-align: center;
        font-size: 12em;
        text-transform: uppercase;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        /*border: 1px solid black;*/
        /*height: 100%;*/
    }
</style>
