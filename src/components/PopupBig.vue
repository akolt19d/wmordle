<template>
    <div id="popup-wrapper">
        <div class="popup" :id="type" v-if="type == 'victoryScreen'">
            <h2>O mój czarnusiu!</h2>
            <p>Wygrałeś, kliknij przycisk pod spodem, aby skopiować śmieszne emotki.</p>
            <button @click="copy">Siare</button>
        </div>
        <div class="popup" :id="type" v-if="type == 'helpPopup'">
            <button @click="toggle">X</button>
            <div>
                <h3>JAK GRAĆ</h3><br>
                <p>
                    Odgadnij <b>Wmordle</b> w SZEŚCIU próbach hehe
                </p><br>
                <p>
                    Każdy strzał musi być pięcioliterowym słowem. Nie mamy systemu weryfikacji słów, ale prosimy, abyś nie był pizdą i używał istniejących słów.
                </p><br>
                <p>
                    Po każdym strzale, kolory kafelków zmienią się w zależności od tego, jak blisko odgadnięcia słowa byłeś.
                </p>
            </div>
            <div>
                <h4>Przykłady</h4>
                <span class="tiles">
                    <span class="green">M</span>
                    <span>O</span>
                    <span>R</span>
                    <span>Y</span>
                    <span>S</span>
                </span>
                <p>Litera M jest w dobrym miejscu.</p>
                <span class="tiles">
                    <span>J</span>
                    <span>E</span>
                    <span class="yellow">B</span>
                    <span>A</span>
                    <span>Ć</span>
                </span>
                <p>Litera B znajduje się w słowie, ale w innym miejscu.</p>
                <span class="tiles">
                    <span>G</span>
                    <span class="gray">R</span>
                    <span>E</span>
                    <span>G</span>
                    <span>A</span>
                </span>
                <p>Litera R nie znajduje sie w słowie.</p>
            </div>
            <h4>W teorii codziennie będzie nowe słowo! (y)</h4>
        </div>
    </div>
</template>

<script>
export default {
    name: "PopupBig",
    props: {
        type: {
            type: String
        }
    },
    methods: {
        toggle() {
            this.$emit('toggle')
        },
        copy() {
            this.$emit('copy')
        }
    }
}
</script>

<style lang="scss" scoped>
#popup-wrapper
{
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    @include fc;
    background-color: rgba(#000, .3);
    backdrop-filter: blur(3px);
    .popup 
    {
        width: 500px;
        max-width: 90%;
        min-height: 550px;
        background-color: $bg;
        border-radius: 5px;
        border: .3px solid rgba($secondary, .1);
        padding: 15px;
        position: relative;
    }
    #helpPopup 
    {
        font-size: 85%;
        h3 
        {
            text-align: center;
        }
        div 
        {
            margin: 10px 0;
        }
        div:nth-of-type(2)
        {
            padding: 15px;
            border-top: .3px solid rgba($secondary, .5);
            border-bottom: .3px solid rgba($secondary, .5);
        }
        button 
        {
            border: 0;
            background: transparent;
            color: $secondary;
            position: absolute;
            right: 10px;
            top: 10px;
            cursor: pointer;
        }
        .tiles 
        {
            margin: 10px 0;
            height: 40px;
            display: grid;
            grid-template-columns: repeat(5, 40px);
            gap: 5px;
            span 
            {
                @include fc;
                border: .3px solid rgba($secondary, .5);
                font-weight: bold;
            }
            .green 
            {
                background-color: $accent;
                color: #1b1b1b;
            }
            .yellow 
            {
                background-color: $yellow;
                color: #1b1b1b;
            }
            .gray 
            {
                background-color: rgba($secondary, .5);
            }
        }
    }
    #victoryScreen
    {
        @include fc;
        flex-direction: column;
        text-align: center;
        font-size: 150%;
        * 
        {
            margin: 15px;
        }
        h2 
        {
            color: $accent;
        }
        button 
        {
            background: $accent;
            font-weight: bold;
            color: #1b1b1b;
            width: 200px;
            height: 60px;
            border: 0;
            font-size: 120%;
            cursor: pointer;
            transition: .2s background;
            &:active
            {
                background: darken($accent, $amount: 30);
            }
        }
    }
}
</style>