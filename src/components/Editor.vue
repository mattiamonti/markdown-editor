<script>
import Menu from './Menu.vue'
export default {
    data() {
        return {
            input: localStorage.getItem('note-input'),
            output: localStorage.getItem('note'),
        }
    },
    components: {
        Menu,
    },
    methods: {
        compiledMarkdown(text) {
            const toHTML = text
                .replace(/^### (.*$)/gim, '<h3>$1</h3>') // h3 tag
                .replace(/^## (.*$)/gim, '<h2>$1</h2>') // h2 tag
                .replace(/^# (.*$)/gim, '<h1>$1</h1>') // h1 tag
                .replace(/\*\*(.*)\*\*/gim, '<b>$1</b>') // bold text
                .replace(/\*(.*)\*/gim, '<i>$1</i>') // italic text
                .replace(/\n\n/gim, '<br /><br />')
            this.output = toHTML.trim()
            localStorage.setItem('note-input', text)
            localStorage.setItem('note', this.output)
            //return toHTML.trim(); // using trim method to remove whitespace

        },

    },
}
</script>

<template>
    <section>
        <Menu></Menu>
        <div id="editor">
            <textarea @input="compiledMarkdown(input)" v-model="input"></textarea>
            <div v-html="output"></div>
        </div>
    </section>

</template>

<style scoped>
#editor {
    margin: 0;
    height: 97vh;
    font-family: "Helvetica Neue", Arial, sans-serif;
}

textarea,
#editor div {
    display: inline-block;
    width: 49%;
    height: 100%;
    vertical-align: top;
    box-sizing: border-box;
    padding: 1.5em 1.5em;
}

#editor div {
    overflow-y: scroll;
}

textarea {
    border: none;
    border-right: 1px solid #ccc;
    resize: none;
    outline: none;
    background-color: #f6f6f6;
    font-size: 0.9em;
    font-family: "Monaco", courier, monospace;
    padding: 1.5em;
}

@media (prefers-color-scheme: dark) {
    textarea {
        background-color: #343434;
        border-color: #545454;
    }

}
</style>