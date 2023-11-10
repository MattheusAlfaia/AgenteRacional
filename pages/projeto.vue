<template>
    <h1>Agente Racional</h1>
    <div class="conffeti">
        <!-- confete -->
    </div>
    <button>Iniciar Limpeza</button>
    <div class="container">
        <div class="robopos"></div>
        <div class="ambiente">
            <div class="localizacao"></div>
        </div>
        <div class="infos">
            <p>🔋: 100%</p>
            <p>🧹</p>
            <p>🎒: 1</p>
        </div>
    </div>
</template>

<style scoped>

button {
    margin: 0 auto;
    display: block;
    margin-bottom: 20px;
    padding: 1rem;
    border-radius: 5px;
    border: 1px solid #000;
    background-color: #fff;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
}

button:hover {
    background-color: rgb(33, 205, 42);
    border: 1px solid #FFF;
    color: #000;
}

button:disabled {
    background-color: #919191;
    border: 1px solid #919191;
    color: #FFF;
    cursor: not-allowed;
}

.container {
    width: 400px;
    margin: 0 auto;
}

.ambiente {
    display: grid;
    grid-template-columns: repeat(4, 100px);
}

.localizacao {
    width: 100px;
    height: 100px;
    border: 1px solid #919191;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 20px;
    font-weight: bold;
    transition: all 1s ease-in-out;
}

.robopos {
    position: absolute;
    background-size: cover;
    background-position: center;
    border-radius: 50px;
    box-shadow: rgba(0, 0, 0, 0.6) 0px 0px 10px;
    width: 6rem;
    height: 6rem;
    transition: all 0.5s ease-in-out;
}


.infos {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
}
</style>