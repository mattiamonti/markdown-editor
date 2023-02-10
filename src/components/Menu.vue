<script>
export default {
    methods: {
        showMenu() {
            const menu = document.getElementById('menu-container')
            const bkblr = document.getElementById('background-blur')
            const btn_menu = document.getElementById('menu')
            var classes = menu.classList
            if (classes.contains('hide')) {
                classes.remove('hide')
                classes.add('show')
                bkblr.classList.remove('hide')
                btn_menu.innerText = 'Close'
            } else {
                classes.remove('show')
                classes.add('hide')
                bkblr.classList.add('hide')
                btn_menu.innerText = 'Menu'
            }

        },
        saveNote() {
            const file = new Blob([localStorage.getItem('note-input').toString()], { type: 'text/md' });
            const link = document.getElementById('link')
            link.href = URL.createObjectURL(file)
        },
        clear() {
            localStorage.setItem('note-input', '# title')
            localStorage.setItem('note', '')
            location.reload()
        }
    }
}
</script>

<template>
    <button id="menu" @click="showMenu()">Menu</button>
    <div class="menu hide" id="menu-container">
        <div class="button-wrapper">
            <a id="link" download="file.md" @click="saveNote()"><button>Download file</button></a>
            <button @click="clear()">Clear</button>
        </div>
    </div>
    <div class="background-blur hide" id="background-blur" @click="showMenu()"></div>
</template>

<style scoped>
button#menu {
    position: absolute;
    right: 1em;
    z-index: 10;
}

.menu {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    width: 30%;
    height: 30%;
    border-radius: 10px;
    right: 50%;
    top: 20%;
    transform: translate(50%, 50%);
    background-color: #424242;
    z-index: 5;
    font-size: 1.25em;

}

.button-wrapper a,
.button-wrapper button {
    display: block;
    margin: 0 auto;
}

.button-wrapper button {
    margin-top: 2em;
}

.hide {
    display: none;

}

.show {
    display: flex;

}

.background-blur {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.1);
    -webkit-backdrop-filter: blur(5px);
    backdrop-filter: blur(5px);
}
</style>