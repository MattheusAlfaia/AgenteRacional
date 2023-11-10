<template>
    <h1>Agente Racional</h1>
    <div class="conffeti">
        <ConfettiExplosion v-if="visible" :duration="5000" :particleCount="250" :force="0.3" />
    </div>
    <button @click="moverRobo" :disabled="iniciado">Iniciar Limpeza</button>
    <div class="container">
        <div class="robopos" :style="roboStyle"
            :class="limpando == 1 ? 'robo-limpando' : '', energia == 0 ? 'robo-capacidade' : ''"></div>
        <div class="ambiente" :class="{ concluido: ObjetivoConcluido }">
            <div v-for="localizacao in mapa" :key="localizacao.name" class="localizacao"
                :class="{ suja: localizacao.suja }">
                {{ localizacao.name }}</div>
        </div>
        <div class="infos">
            <p>🔋: {{ energia }}%</p>
            <p v-if="info">{{ info }}</p>
            <p>🎒: {{ bolsa }}</p>
        </div>
    </div>
</template>

<script>
import { nextTick, ref } from "vue";
import ConfettiExplosion from "vue-confetti-explosion";
import robo from '@/assets/img/robo.png';
export default {
    mounted() {
        window.addEventListener('keydown', this.handleKeyDown);
    },
    beforeUnmount() {
        window.removeEventListener('keydown', this.handleKeyDown);
    },
    components: {
        ConfettiExplosion,
    },
    setup() {
        const visible = ref(false);
        const explode = async () => {
            visible.value = false;
            await nextTick();
            visible.value = true;
        };
        return {
            visible,
            explode,
        };
    },
    data() {
        return {
            mapa: [
                { name: 'A', suja: false },
                { name: 'B', suja: false },
                { name: 'C', suja: true },
                { name: 'D', suja: false },
                { name: 'E', suja: false },
                { name: 'F', suja: true },
                { name: 'G', suja: false },
                { name: 'H', suja: true },
                { name: 'I', suja: true },
                { name: 'J', suja: false },
                { name: 'K', suja: true },
                { name: 'L', suja: false },
                { name: 'M', suja: true },
                { name: 'N', suja: false },
                { name: 'O', suja: true },
                { name: 'P', suja: false },
            ],
            iniciado: false,
            energia: 100,
            bolsa: 0,
            roboX: 0,
            roboY: 0,
            limpando: 0,
            direcoesAnterior: null,
            ObjetivoConcluido: false,
            confettiActive: false,
            info: null,
        }
    },
    computed: {
        roboStyle() {
            return {
                transform: `translate(${this.roboX * 100}px, ${this.roboY * 100}px)`,
                backgroundImage: `url(${robo})`,
            };
        },
    },
    methods: {
        async moverRobo() {
            this.iniciado = true;
            while (this.ObjetivoConcluido == false) {
                if (this.energia === 0) {
                    this.ObjetivoConcluido = true;
                }
                await new Promise(resolve => setTimeout(resolve, 1000));

                this.energia--;

                const sujoMaisProximo = this.mapa
                    .filter(localizacao => localizacao.suja)
                    .sort((a, b) => {
                        const distanciaA = Math.abs(this.roboX - this.mapa.indexOf(a) % 4) + Math.abs(this.roboY - Math.floor(this.mapa.indexOf(a) / 4));
                        const distanciaB = Math.abs(this.roboX - this.mapa.indexOf(b) % 4) + Math.abs(this.roboY - Math.floor(this.mapa.indexOf(b) / 4));
                        return distanciaA - distanciaB;
                    })[0];

                const localizacao = this.mapa.find(localizacao => localizacao.name === sujoMaisProximo.name);
                const destinoX = this.mapa.indexOf(localizacao) % 4;
                const destinoY = Math.floor(this.mapa.indexOf(localizacao) / 4);

                const moveRobo = () => {
                    if (this.roboX !== destinoX || this.roboY !== destinoY) {
                        if (this.roboX > destinoX) {
                            this.roboX--;
                            this.energia--;
                            this.info = '👈';
                        } else if (this.roboX < destinoX) {
                            this.roboX++;
                            this.energia--;
                            this.info = '👉';
                        } else if (this.roboY > destinoY) {
                            this.roboY--;
                            this.energia--;
                            this.info = '👆';
                        } else if (this.roboY < destinoY) {
                            this.roboY++;
                            this.energia--;
                            this.info = '👇';
                        }

                        setTimeout(moveRobo, 1000);
                    }
                };

                moveRobo();

                if (this.mapa[this.roboY * 4 + this.roboX].suja) {
                    this.mapa[this.roboY * 4 + this.roboX].suja = false;
                    this.limpando = 1;
                    this.bolsa++;
                    this.energia--;
                    setTimeout(() => {
                        this.limpando = 0;
                    }, 1000);
                }

                if (this.bolsa === 7) {
                    const moveBack = () => {
                        if (this.roboX > 0) {
                            this.roboX--;
                            this.energia--;
                        }
                        if (this.roboY > 0) {
                            this.roboY--;
                            this.energia--;
                        }
                        if (this.roboX > 0 || this.roboY > 0) {
                            setTimeout(moveBack, 1000);
                        }
                    };
                    setTimeout(moveBack, 1000);
                    this.ObjetivoConcluido = true;
                    this.info = '👌';
                    this.concluido();
                }
            }
        },
        async concluido() {
            await new Promise(resolve => setTimeout(resolve, 4400));
            if (this.bolsa === 7 && this.roboX === 0 && this.roboY === 0) {
                this.bolsa = 0;
                this.energia = 100;
                this.info = null;
            }
            this.explode();
            await new Promise(resolve => setTimeout(resolve, 4000));
            this.ObjetivoConcluido = false;

            this.mapa[2].suja = true;
            this.mapa[5].suja = true;
            this.mapa[7].suja = true;
            this.mapa[8].suja = true;
            this.mapa[10].suja = true;
            this.mapa[12].suja = true;
            this.mapa[14].suja = true;
            this.iniciado = false;
        },
        handleKeyDown(event) {
            switch (event.key) {
                case 'w':
                    if (this.roboY == 0) {
                        this.roboY = 0;
                    } else {
                        this.roboY--;
                    }
                    break;
                case 'a':
                    if (this.roboX == 0) {
                        this.roboX = 0;
                    } else {
                        this.roboX--;
                    }
                    break;
                case 's':
                    if (this.roboY == 3) {
                        this.roboY = 3;
                    } else {
                        this.roboY++;
                    }
                    break;
                case 'd':
                    if (this.roboX == 3) {
                        this.roboX = 3;
                    } else {
                        this.roboX++;
                    }
                    break;
                default:
                    return;
            }
        }
    }
}
</script>

<style scoped>
.concluido {
    color: #FFF;
    background: linear-gradient(45deg, #FFC107, #FF9800, #FF5722, #F44336, #E91E63, #9C27B0, #673AB7, #3F51B5, #2196F3, #03A9F4, #00BCD4, #009688, #4CAF50, #8BC34A, #CDDC39, #FFEB3B);
    background-size: 200% 200%;
    animation: animacao 8s ease infinite;
}

@keyframes animacao {
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

h1 {
    text-align: center;
}

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

.conffeti {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
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

.suja {
    background-image: url("@/assets/img/lata.png");
    background-size: cover;
    background-position: center;
}

.robopos {
    position: absolute;
    background-size: cover;
    background-position: center;
    border-radius: 50px;
    box-shadow: rgba(0, 0, 0, 0.8) 0px 0px 10px;
    width: 6rem;
    height: 6rem;
    transition: all 0.5s ease-in-out;
}


.robo-limpando {
    box-shadow: rgba(92, 17, 255, 0.6) 0px 0px 20px;
}

.robo-capacidade {
    background-color: #0a7894;
    border-radius: 40px;
    border: 2px solid rgb(205, 33, 33);
    width: 6rem;
    height: 6rem;
    animation: capacidade 1s ease-in-out infinite;
}

@keyframes capacidade {
    0% {
        background-color: #0a7894;
    }

    50% {
        background-color: rgb(205, 33, 33);
    }

    100% {
        background-color: #0a7894;
    }
}

.infos {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
}
</style>