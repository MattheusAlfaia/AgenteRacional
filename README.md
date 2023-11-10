# Sistema do Agente Aspirador com Interface Gráfica

Este é um sistema do agente aspirador com uma interface gráfica que visa proporcionar uma limpeza eficiente em um ambiente dinâmico. O agente aspirador opera em um grid 4x4 (16 locais) onde cada local pode estar limpo ou sujo. A eficiência da limpeza é medida pela quantidade total de sujeira aspirada pelo agente, com o desempenho ideal sendo a manutenção do ambiente completamente limpo.

## Características do Sistema

### Limpeza Eficiente
A eficiência da limpeza é medida pela quantidade total de sujeira aspirada pelo agente. O objetivo é manter o ambiente completamente limpo.

### Capacidade da Bolsa de Sujeira
A bolsa de sujeira tem capacidade para armazenar 10 unidades de sujeira. O agente deve esvaziar a bolsa quando estiver cheia para continuar aspirando. Se a bolsa atingir sua capacidade máxima, o agente deve retornar ao local de partida e esvaziar a bolsa para continuar a limpeza.

### Ambiente
O ambiente é um grid 4x4 com 16 locais, cada um podendo estar limpo (false) ou sujo (true). A sujeira é distribuída conforme as especificações do documento fornecido. O ambiente é dinâmico, pois o agente limpa a sujeira, alterando o estado do ambiente para limpo.

### Atuadores
- **Motores de Movimentação:** Permitem que o agente se mova para cima, para baixo, para a esquerda ou para a direita no local.
- **Mecanismo de Sucção:** Permite que o agente aspire a sujeira presente no local atual.

### Sensores
- **Sensores de Posição:** Informam a posição atual do agente no local 4x4.
- **Sensores de Sujeira:** Analisam se a posição atual está limpa ou suja.
- **Nível de Energia:** Indica a quantidade de energia restante para o agente.
- **Nível de Energia em Tempo Real:** Mostra a diminuição de energia do agente em tempo real.
- **Contador de Bolsa:** Indica quantas unidades de sujeira o agente coletou na bolsa.

## Instruções de Uso

1. **Execução do Programa:** Execute o programa do agente aspirador com interface gráfica.
2. **Monitoramento:** Acompanhe o desempenho do agente por meio da visualização gráfica e dos indicadores de limpeza.
3. **Intervenção Manual:** Se necessário, intervenha manualmente para esvaziar a bolsa quando estiver cheia.

Com estas funcionalidades, o Sistema do Agente Aspirador proporciona uma abordagem eficaz para a limpeza de ambientes dinâmicos, garantindo que o local seja mantido limpo e a bolsa de sujeira seja gerenciada adequadamente.


# Como Iniciar a Aplicação NuxtJs 3
## Clone este repositório
~$ git clone
## Acesse a pasta do projeto
cd nome_da_pasta
## Instale as dependências
~$ npm install
## Execute a aplicação em modo de desenvolvimento
$ npm run dev