<template>
    <div class="layout">
        <header>
            <slot name="header"></slot>
        </header>
        <aside>
            <slot name="aside"></slot>
        </aside>
        <main>
            <slot name="main"></slot>
        </main>
        <footer>
            <slot name="footer"></slot>
        </footer>
    </div>
</template>

<style>
.layout {
    display: grid; 
    grid-template-columns: 400px 1fr;
    grid-template-rows: 20% 75% 5%;
    min-height: 100vh;   
    background: linear-gradient(rgb(255, 255, 255), rgb(72, 0, 72));
}

.layout header, 
.layout footer {
    /* css pour dire tu commences a la premiere colonne et tu finis à la dernière */
    grid-column: 1 / -1;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding-left: 10px;    
}

.layout header {
    padding-top: 10px;
}

aside {
    overflow-y: auto;
    max-height: 100vh;
    padding-top: 10px;
    padding-bottom: 1Opx;
}

main {
    padding-top: 10px;
    padding-bottom: 1Opx;
}

@media screen and (max-height: 444px) {
    .layout header {
        flex-direction: row;
    } 
}



</style>