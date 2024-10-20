 # Descrição do exercício:

Vamos construir uma Calculadora de Notas que pode calcular médias e verificar o status de aprovação ou reprovação de um aluno. A calculadora permitirá que o usuário insira notas e, em seguida, realizará as operações de soma para calcular a média, além de exibir se o aluno foi aprovado ou reprovado.

Requisitos:
HTML:

Um campo para inserir as notas.
Botões para somar as notas, calcular a média, e verificar a aprovação.
Um campo para mostrar o resultado da média e o status de aprovação/reprovação.
CSS (Tailwind):

Estilizar a interface da calculadora de maneira simples e responsiva.
JavaScript:

Usar um array para armazenar as notas inseridas.
Implementar uma função para calcular a soma das notas e a média.
Usar estruturas de controle como if/else e switch para determinar o status de aprovação.
Um loop para somar as notas e calcular a média.

html:
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Notas</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-200 p-6">

    <div class="container mx-auto bg-white p-6 rounded-lg shadow-lg">
        <h1 class="text-3xl font-semibold mb-6 text-center">Calculadora de Notas</h1>

        <!-- Display da média e status -->
        <div class="mb-4">
            <input id="inputNotas" type="text" class="w-full p-3 text-center text-2xl border border-gray-300 rounded" placeholder="Digite as notas (separadas por vírgula)" readonly>
        </div>

        <!-- Botões para ações -->
        <div class="grid grid-cols-4 gap-4">
            <button class="btn" onclick="adicionarNota('1')">1</button>
            <button class="btn" onclick="adicionarNota('2')">2</button>
            <button class="btn" onclick="adicionarNota('3')">3</button>
            <button class="btn bg-yellow-500" onclick="setOperacao('+')">+</button>

            <button class="btn" onclick="adicionarNota('4')">4</button>
            <button class="btn" onclick="adicionarNota('5')">5</button>
            <button class="btn" onclick="adicionarNota('6')">6</button>
            <button class="btn bg-yellow-500" onclick="setOperacao('-')">-</button>

            <button class="btn" onclick="adicionarNota('7')">7</button>
            <button class="btn" onclick="adicionarNota('8')">8</button>
            <button class="btn" onclick="adicionarNota('9')">9</button>
            <button class="btn bg-yellow-500" onclick="setOperacao('*')">*</button>

            <button class="btn" onclick="adicionarNota('0')">0</button>
            <button class="btn" onclick="limparNotas()">C</button>
            <button class="btn bg-green-500" onclick="calcularMedia()">Calcular Média</button>
            <button class="btn bg-yellow-500" onclick="setOperacao('/')">/</button>
        </div>

        <!-- Exibir a média e o status do aluno -->
        <div class="mt-6 text-center">
            <p id="resultado" class="text-lg font-semibold"></p>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

/* O Tailwind já está aplicando a maior parte da estilização */
.btn {
    background-color: #4CAF50;
    color: white;
    font-size: 1.25rem;
    padding: 15px;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #45a049;
}

// script.js
let notas = [];  // Array para armazenar as notas inseridas
let operacao = '';  // Operação que será aplicada (no caso, sempre soma)

// Função para adicionar nota ao array
function adicionarNota(nota) {
    const inputNotas = document.getElementById('inputNotas');
    inputNotas.value += nota;  // Adiciona o número no campo de input
    notas.push(parseFloat(nota));  // Adiciona a nota ao array
}

// Função para limpar as notas inseridas
function limparNotas() {
    const inputNotas = document.getElementById('inputNotas');
    inputNotas.value = '';
    notas = [];  // Limpa o array de notas
}

// Função para definir a operação (no nosso caso, só soma por enquanto)
function setOperacao(op) {
    operacao = op;  // Define a operação
}

// Função para calcular a média das notas
function calcularMedia() {
    if (notas.length === 0) {
        alert("Por favor, insira ao menos uma nota.");
        return;
    }

    // Soma todas as notas usando um loop
    let soma = 0;
    for (let i = 0; i < notas.length; i++) {
        soma += notas[i];
    }

    // Calcula a média
    let media = soma / notas.length;
    
    // Exibe a média e o status de aprovação ou reprovação
    const resultado = document.getElementById('resultado');
    
    // Condicional para verificar a aprovação (nota mínima 6)
    let status = '';
    if (media >= 6) {
        status = 'Aprovado';
        resultado.style.color = 'green';
    } else {
        status = 'Reprovado';
        resultado.style.color = 'red';
    }

    resultado.innerHTML = `Média: ${media.toFixed(2)} - Status: ${status}`;
    limparNotas();  // Limpa as notas após o cálculo
}

Explicação do Código:
HTML:
Input: Um campo para inserir as notas manualmente.
Botões: Botões numéricos de 0 a 9, além dos botões para limpar (C), calcular a média, e operações aritméticas básicas (que podem ser usadas futuramente se necessário).
Campo de Resultado: Um campo que exibe a média e o status de aprovação ou reprovação.
CSS (Tailwind):
O Tailwind já fornece todas as classes necessárias para estilizar rapidamente o layout.
As classes de botões (btn) utilizam cores como verde, vermelho e amarelo para identificar visualmente as diferentes operações e resultados.
JavaScript:
Array notas: Armazena as notas inseridas pelo usuário.
Funções adicionarNota, limparNotas, setOperacao, calcularMedia:
adicionarNota: Insere a nota no campo de input e no array de notas.
limparNotas: Limpa o campo de input e o array de notas.
setOperacao: Define a operação, mas no momento estamos apenas somando as notas.
calcularMedia: Soma as notas e calcula a média, além de determinar se o aluno foi aprovado (média ≥ 6) ou reprovado (média < 6).
Loop: O loop for percorre o array de notas para somá-las e calcular a média.
Comportamento Esperado:
O usuário insere as notas separadas por vírgulas e clica em "Calcular Média".
A calculadora soma as notas, calcula a média e exibe o status de "Aprovado" ou "Reprovado" no campo de resultado.
O botão "C" limpa o campo de entrada e os resultados.
Extensões Sugeridas:
Adicionar uma funcionalidade para lidar com notas com casas decimais.
Adicionar um campo para inserir o número de disciplinas (para calcular a média ponderada).
Melhorar a interface com mais detalhes usando as classes Tailwind.