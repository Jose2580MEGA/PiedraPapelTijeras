<template>
    <div>
    <header>
    <h1>El Encabezado de Mi App</h1>
    <nav>

    </nav>
    </header>
    <main>
    <slot /> </main>
    <footer>
    <p>&copy; Mi Pie de Página</p>
    </footer>
</div>
</template>

<style scoped>
header {
    background-color: #f0f0f0;
    padding: 20px;
    text-align: center;
}

h1 {
    color: navy;
}

footer {
    background-color: #333;
    color: white;
    padding: 10px;
    text-align: center;
    position: fixed;
    bottom: 0;
    width: 100%;
}
</style>