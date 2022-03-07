<template>
    <button class="key lettera" @click="$emit('typed', 'a')" />
    <button class="key letterb" @click="$emit('typed', 'b')" />
    <button class="key letterc" @click="$emit('typed', 'c')" />
    <button class="key letterd" @click="$emit('typed', 'd')" />
    <button class="key lettere" @click="$emit('typed', 'e')" />
    <button class="key letterf" @click="$emit('typed', 'f')" />
    <button class="key letterg" @click="$emit('typed', 'g')" />
    <button class="key letterh" @click="$emit('typed', 'h')" />
    <button class="key letteri" @click="$emit('typed', 'i')" />
    <br />
    <button class="key letterj" @click="$emit('typed', 'j')" />
    <button class="key letterk" @click="$emit('typed', 'k')" />
    <button class="key letterl" @click="$emit('typed', 'l')" />
    <button class="key letterm" @click="$emit('typed', 'm')" />
    <button class="key lettern" @click="$emit('typed', 'n')" />
    <button class="key lettero" @click="$emit('typed', 'o')" />
    <button class="key letterp" @click="$emit('typed', 'p')" />
    <button class="key letterq" @click="$emit('typed', 'q')" />
    <button class="key letterr" @click="$emit('typed', 'r')" />
    <br />
    <button class="key letters" @click="$emit('typed', 's')" />
    <button class="key lettert" @click="$emit('typed', 't')" />
    <button class="key letteru" @click="$emit('typed', 'u')" />
    <button class="key letterv" @click="$emit('typed', 'v')" />
    <button class="key letterw" @click="$emit('typed', 'w')" />
    <button class="key letterx" @click="$emit('typed', 'x')" />
    <button class="key lettery" @click="$emit('typed', 'y')" />
    <button class="key letterz" @click="$emit('typed', 'z')" />
    <button class="key ok" @click="$emit('typed', 'ok')" />
    <button class="key cancel" @click="$emit('typed', 'clear')" />
</template>

<script>
export default {
    emits: ['typed']
}
</script>

<style>
.ok {
    background: url("./icons/check.png") no-repeat;
}
.cancel {
    background: url("./icons/cancel.png") no-repeat;
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
    width: 40px;
    height: 40px;
    border-radius: 10px;
}
</style>