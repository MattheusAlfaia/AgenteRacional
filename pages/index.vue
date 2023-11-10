<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1>Trabalho de Agente Racional</h1>
                <p>Professor: {{ professor.name }}</p>
                <p>Disciplina: {{ disciplina.name }}</p>
                <p>Curso: {{ curso.name }}</p>
                <div class="alunos">
                    <h2>Alunos</h2>
                    <ul>
                        <li v-for="aluno in alunos" :key="aluno.nome">{{ aluno.nome }}</li>
                    </ul>
                </div>
                <nuxt-link class="btn" to="/projeto">Ir Para Trabalho</nuxt-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data() { 
        return {
            professor: { name: 'Thiago Figueira' },
            disciplina: { name: 'Tópicos Especiais II' },
            curso: { name: 'Sistemas de Informação 8º período' },
            alunos: [
                { nome: 'Mattheus Cruz' },
                { nome: 'Leandro Santos' },
                { nome: 'Flávio Solon' },
                { nome: 'César Augusto' }
            ],
        }
    }
};
</script>

<style scoped>
body{
    font-size: 1.8rem;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.container{
    background: linear-gradient(90deg, rgb(8, 180, 71) 0%, rgb(9, 58, 121) 35%, rgb(87, 25, 230) 100%);
    background-size: 500% 400%;
    animation: gradient 8s ease infinite;
    color: #FFF;
    width: 100%;
    height: 100vh;
}

@keyframes gradient {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}

.row{
    display: flex;
    justify-content: center;
}

.col-12 {
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
}

h1 {
    font-size: 3rem;
}

.alunos{
    text-align: center;
    animation: textFlutuando 8s ease infinite;
}

h2{
    font-size: 2rem;
    margin: 0;
}

ul{
    list-style: none;
    padding: 0;
    margin: 0;
}

ul li{
    font-size: 1.5rem;
    margin: 0.5rem;
}

.btn {
    margin-top: 2rem;
    padding: 1rem 2rem;
    border-radius: 10px;
    background-color: rgb(24, 42, 57);
    color: white;
    font-weight: bold;
    font-size: 1.2rem;
    border: none;
    text-decoration: none;
}

.btn:hover {
    background-color: rgb(33, 205, 42);
    color: black;
}
</style>