<template>
    <div class="keyboard">
        <div class="keys">
            <div class="firstrow">
                <button class="key lettera" @click="$emit('typed', 'a')" />
                <button class="key letterz" @click="$emit('typed', 'z')" />
                <button class="key lettere" @click="$emit('typed', 'e')" />
                <button class="key letterr" @click="$emit('typed', 'r')" />
                <button class="key lettert" @click="$emit('typed', 't')" />
                <button class="key lettery" @click="$emit('typed', 'y')" />
                <button class="key letteru" @click="$emit('typed', 'u')" />
                <button class="key letteri" @click="$emit('typed', 'i')" />
                <button class="key lettero" @click="$emit('typed', 'o')" />
                <button class="key letterp" @click="$emit('typed', 'p')" />
            </div>
            <div class="secondrow">
                <button class="key letterq" @click="$emit('typed', 'q')" />
                <button class="key letters" @click="$emit('typed', 's')" />
                <button class="key letterd" @click="$emit('typed', 'd')" />
                <button class="key letterf" @click="$emit('typed', 'f')" />
                <button class="key letterg" @click="$emit('typed', 'g')" />
                <button class="key letterh" @click="$emit('typed', 'h')" />
                <button class="key letterj" @click="$emit('typed', 'j')" />
                <button class="key letterk" @click="$emit('typed', 'k')" />
                <button class="key letterl" @click="$emit('typed', 'l')" />
                <button class="key letterm" @click="$emit('typed', 'm')" />
            </div>
            <div class="lastrow">
                <button class="key letterw" @click="$emit('typed', 'w')" />
                <button class="key letterx" @click="$emit('typed', 'x')" />
                <button class="key letterc" @click="$emit('typed', 'c')" />
                <button class="key letterv" @click="$emit('typed', 'v')" />
                <button class="key letterb" @click="$emit('typed', 'b')" />
                <button class="key lettern" @click="$emit('typed', 'n')" />
            </div>
        </div>
        <div class="submit">
            <button class="ok" @click="$emit('typed', 'ok')" />
        </div>
    </div>
</template>

<script>
export default {
    emits: ['typed']
}
</script>

<style>
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
