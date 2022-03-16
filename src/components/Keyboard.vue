<template>
    <div class="keyboard">
        <div class="keys">
            <div class="firstrow">
                <button
                    :disabled="this.disabledMap['A']"
                    class="key lettera"
                    @click="$emit('typed', 'A')"
                />
                <button
                    :disabled="this.disabledMap['Z']"
                    class="key letterz"
                    @click="$emit('typed', 'Z')"
                />
                <button
                    :disabled="this.disabledMap['E']"
                    class="key lettere"
                    @click="$emit('typed', 'E')"
                />
                <button
                    :disabled="this.disabledMap['R']"
                    class="key letterr"
                    @click="$emit('typed', 'R')"
                />
                <button
                    :disabled="this.disabledMap['T']"
                    class="key lettert"
                    @click="$emit('typed', 'T')"
                />
                <button
                    :disabled="this.disabledMap['Y']"
                    class="key lettery"
                    @click="$emit('typed', 'Y')"
                />
                <button
                    :disabled="this.disabledMap['U']"
                    class="key letteru"
                    @click="$emit('typed', 'U')"
                />
                <button
                    :disabled="this.disabledMap['I']"
                    class="key letteri"
                    @click="$emit('typed', 'I')"
                />
                <button
                    :disabled="this.disabledMap['O']"
                    class="key lettero"
                    @click="$emit('typed', 'O')"
                />
                <button
                    :disabled="this.disabledMap['P']"
                    class="key letterp"
                    @click="$emit('typed', 'P')"
                />
            </div>
            <div class="secondrow">
                <button
                    :disabled="this.disabledMap['Q']"
                    class="key letterq"
                    @click="$emit('typed', 'Q')"
                />
                <button
                    :disabled="this.disabledMap['S']"
                    class="key letters"
                    @click="$emit('typed', 'S')"
                />
                <button
                    :disabled="this.disabledMap['D']"
                    class="key letterd"
                    @click="$emit('typed', 'D')"
                />
                <button
                    :disabled="this.disabledMap['F']"
                    class="key letterf"
                    @click="$emit('typed', 'F')"
                />
                <button
                    :disabled="this.disabledMap['G']"
                    class="key letterg"
                    @click="$emit('typed', 'G')"
                />
                <button
                    :disabled="this.disabledMap['H']"
                    class="key letterh"
                    @click="$emit('typed', 'H')"
                />
                <button
                    :disabled="this.disabledMap['J']"
                    class="key letterj"
                    @click="$emit('typed', 'J')"
                />
                <button
                    :disabled="this.disabledMap['K']"
                    class="key letterk"
                    @click="$emit('typed', 'K')"
                />
                <button
                    :disabled="this.disabledMap['L']"
                    class="key letterl"
                    @click="$emit('typed', 'L')"
                />
                <button
                    :disabled="this.disabledMap['M']"
                    class="key letterm"
                    @click="$emit('typed', 'M')"
                />
            </div>
            <div class="lastrow">
                <button
                    :disabled="this.disabledMap['W']"
                    class="key letterw"
                    @click="$emit('typed', 'W')"
                />
                <button
                    :disabled="this.disabledMap['X']"
                    class="key letterx"
                    @click="$emit('typed', 'X')"
                />
                <button
                    :disabled="this.disabledMap['C']"
                    class="key letterc"
                    @click="$emit('typed', 'C')"
                />
                <button
                    :disabled="this.disabledMap['V']"
                    class="key letterv"
                    @click="$emit('typed', 'V')"
                />
                <button
                    :disabled="this.disabledMap['B']"
                    class="key letterb"
                    @click="$emit('typed', 'B');"
                />
                <button
                    :disabled="this.disabledMap['N']"
                    class="key lettern"
                    @click="$emit('typed', 'N')"
                />
            </div>
        </div>
        <div class="submit">
            <button class="ok" @click="okBtnClicked" />
        </div>
    </div>
</template>

<script>
export default {
    props: ['letter'],
    data() {
        return {
            disabledMap: {
                'A': false, 'B': false, 'C': false, 'D': false, 'E': false, 'F': false,
                'G': false, 'H': false, 'I': false, 'J': false, 'K': false, 'L': false,
                'M': false, 'N': false, 'O': false, 'P': false, 'Q': false, 'R': false,
                'S': false, 'T': false, 'U': false, 'V': false, 'W': false, 'X': false,
                'Y': false, 'Z': false
            }
        }
    },
    emits: ['typed'],
    methods: {
        okBtnClicked() {
            this.disabledMap[this.letter] = true
            this.storeKeyboardState()
            this.$emit('typed', 'ok')
        },
        storeKeyboardState() {
            let date = new Date();
            var midnight = new Date(date.getFullYear(), date.getMonth(), date.getDate(), 23, 59, 59);
            document.cookie = "keyboard" + "=" + JSON.stringify(this.disabledMap) + ";expires=" + midnight.toUTCString();
        },
        readKeyboardState() {
            var keyStr = this.getCookie("keyboard")
            if (keyStr != "") {
                this.disabledMap = JSON.parse(keyStr)
            }
        },
        getCookie(cname) {
            let name = cname + "=";
            let ca = document.cookie.split(';');
            for (let i = 0; i < ca.length; i++) {
                let c = ca[i];
                while (c.charAt(0) == ' ') {
                    c = c.substring(1);
                }
                if (c.indexOf(name) == 0) {
                    return c.substring(name.length, c.length);
                }
            }
            return "";
        }
    },
    mounted() {
        this.readKeyboardState()
    }
}
</script>

<style>
button:disabled {
    background-color: #ffffff;
}
.ok {
    background: url("./icons/check.png") no-repeat;
    width: 80px;
    height: 80px;
    background-size: cover;
    border-radius: 10px;
}
.lettera {
    background: url("./icons/letters/lettera.png") no-repeat;
}
.letterb {
    background: url("./icons/letters/letterb.png") no-repeat;
}
.letterc {
    background: url("./icons/letters/letterc.png") no-repeat;
}
.letterd {
    background: url("./icons/letters/letterd.png") no-repeat;
}
.lettere {
    background: url("./icons/letters/lettere.png") no-repeat;
}
.letterf {
    background: url("./icons/letters/letterf.png") no-repeat;
}
.letterg {
    background: url("./icons/letters/letterg.png") no-repeat;
}
.letterh {
    background: url("./icons/letters/letterh.png") no-repeat;
}
.letteri {
    background: url("./icons/letters/letteri.png") no-repeat;
}
.letterj {
    background: url("./icons/letters/letterj.png") no-repeat;
}
.letterk {
    background: url("./icons/letters/letterk.png") no-repeat;
}
.letterl {
    background: url("./icons/letters/letterl.png") no-repeat;
}
.letterm {
    background: url("./icons/letters/letterm.png") no-repeat;
}
.lettern {
    background: url("./icons/letters/lettern.png") no-repeat;
}
.lettero {
    background: url("./icons/letters/lettero.png") no-repeat;
}
.letterp {
    background: url("./icons/letters/letterp.png") no-repeat;
}
.letterq {
    background: url("./icons/letters/letterq.png") no-repeat;
}
.letterr {
    background: url("./icons/letters/letterr.png") no-repeat;
}
.letters {
    background: url("./icons/letters/letters.png") no-repeat;
}
.lettert {
    background: url("./icons/letters/lettert.png") no-repeat;
}
.letteru {
    background: url("./icons/letters/letteru.png") no-repeat;
}
.letterv {
    background: url("./icons/letters/letterv.png") no-repeat;
}
.letterw {
    background: url("./icons/letters/letterw.png") no-repeat;
}
.letterx {
    background: url("./icons/letters/letterx.png") no-repeat;
}
.lettery {
    background: url("./icons/letters/lettery.png") no-repeat;
}
.letterz {
    background: url("./icons/letters/letterz.png") no-repeat;
}
.key {
    background-size: cover;
    width: 30px;
    height: 30px;
    border-radius: 10px;
}
.keys {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    align-content: center;
    gap: 10px;
}

.keyboard {
    width: 360px;
    display: flex;
    flex-direction: column;
    gap: 15px;
    justify-content: center;
    align-items: center;
}

.firstrow {
    display: inline-flex;
    gap: 8px;
}
.secondrow {
    display: inline-flex;
    gap: 8px;
}
.lastrow {
    display: inline-flex;
    gap: 8px;
}
</style>
