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
    grid-template-rows: 25% 75% 10%;
    min-height: 100vh;
}

.layout header, 
.layout footer {
    /* css pour dire tu commences a la premiere colonne et tu finis à la dernière */
    grid-column: 1 / -1;
}


</style>