# DevLingo Arena

## Criando um Jogo Educacional em JavaScript com Node.js e readline-sync

---

# 1. Objetivo do Projeto

Neste projeto vamos desenvolver um jogo de terminal chamado **DevLingo Arena**.

Ele será um jogo educativo para praticar inglês, utilizando:

* Node.js
* JavaScript
* Biblioteca readline-sync
* Estrutura modular (arquivos separados)
* Sistema de pontuação
* Sistema de vidas
* Menu interativo

Além de aprender inglês, nós vamos praticar:

* Organização de projeto
* Modularização
* Funções
* Arrays e objetos
* Estruturas de decisão
* Loops
* Manipulação de estado

Mas o que é este projeto? Nós estamos estudando inglês com foco no nosso mundo, o do desenvolvimento. Para isso, nada melhor do que aplicarmos ele
na prática: codando!
Por isso, vamos criar o DevLingo: um projeto que inclui diversos jogos diferentes, todos voltados para o ensino de inglês. Cada jogo tem regras 
diferentes, ensinando de maneiras diferentes. Vamos utilizar o JavaScript, linguagem que aprendemos anteriormente na UC2, e toda a interação
com os jogos vai ser feita diretamente via terminal, através de uma biblioteca chamada readline-sync. Bora?


---

# 2. Criando o Projeto

## 2.1 Criar a pasta do projeto

```
mkdir DevLingo-Arena
cd DevLingo-Arena
```

## 2.2 Inicializar o projeto Node

```
npm init -y
```

Esse comando cria o arquivo:

```
package.json
```

Ele armazena informações do projeto e dependências.

---

# 3. Instalando readline-sync

Nosso jogo precisa receber entrada do usuário no terminal.

O Node.js puro não é ideal para isso de forma simples.
Por isso usamos a biblioteca `readline-sync`.

Instale com:

```
npm install readline-sync
```

Agora o projeto tem a pasta:

```
node_modules/
```

E o package.json terá:

```
"dependencies": {
  "readline-sync": "^..."
}
```

---

# 4. Estrutura do Projeto

Crie a seguinte estrutura:

```
DevLingo-Arena/
│
├── index.js
├── menu.js
├── gameState.js
│
└── games/
    ├── quiz.js
    ├── completeSentence.js
    ├── sentenceBuilder.js
    ├── memoryChallenge.js
    ├── battleRPG.js
    └── detectiveStory.js
```

Crie a pasta `games` manualmente.

---

# 5. Entendendo a Arquitetura

Teremos:

* index.js → ponto de entrada
* menu.js → controla o fluxo principal
* gameState.js → controla pontuação e vidas
* games/ → cada jogo separado em um módulo

Essa organização evita código bagunçado.

---

# 6. Criando o Estado do Jogo

Arquivo: gameState.js

Responsável por controlar score e vidas.

```js
// Variáveis internas do módulo
let score = 0;
let lives = 3;

// Adiciona pontos
function addScore(points) {
    score += points;
}

// Remove uma vida
function loseLife() {
    lives--;
}

// Retorna pontuação atual
function getScore() {
    return score;
}

// Retorna vidas atuais
function getLives() {
    return lives;
}

// Reinicia o jogo
function resetGame() {
    score = 0;
    lives = 3;
}

// Exportamos as funções
module.exports = {
    addScore,
    loseLife,
    getScore,
    getLives,
    resetGame
};
```

Importante:
Estamos usando `module.exports` para permitir que outros arquivos utilizem essas funções.

---

# 7. Criando o Menu Principal

Arquivo: menu.js

```js
const readline = require('readline-sync');
const gameState = require('./gameState');

// Importando os jogos
const quiz = require('./games/quiz');
const completeSentence = require('./games/completeSentence');
const sentenceBuilder = require('./games/sentenceBuilder');
const memoryChallenge = require('./games/memoryChallenge');
const battleRPG = require('./games/battleRPG');
const detectiveStory = require('./games/detectiveStory');

function showMenu() {

    // Loop infinito: o menu sempre volta
    while (true) {

        // Verifica se o jogador perdeu todas as vidas
        if (gameState.getLives() <= 0) {
            console.log("\nGAME OVER");
            console.log("Final Score:", gameState.getScore());
            gameState.resetGame();
        }

        console.log("\n==== DEVLINGO ARENA ====");
        console.log("Score:", gameState.getScore(), "| Lives:", gameState.getLives());
        console.log("1 - Quiz");
        console.log("2 - Complete the Sentence");
        console.log("3 - Sentence Builder");
        console.log("4 - Memory Challenge");
        console.log("5 - Battle RPG");
        console.log("6 - Detective Story");
        console.log("0 - Exit");

        let option = readline.question("Choose an option: ");

        switch(option) {
            case "1": quiz(); break;
            case "2": completeSentence(); break;
            case "3": sentenceBuilder(); break;
            case "4": memoryChallenge(); break;
            case "5": battleRPG(); break;
            case "6": detectiveStory(); break;
            case "0": process.exit();
            default:
                console.log("Invalid option.");
        }
    }
}

module.exports = showMenu;
```

Observe:

* Usamos `while(true)` para manter o menu ativo.
* Cada jogo executa e retorna.
* O menu controla o fluxo.

---

# 8. Arquivo Principal

Arquivo: index.js

```js
const showMenu = require('./menu');

// Limpa o terminal
console.clear();

// Inicia o programa
showMenu();
```

Execute com:

```
node index.js
```

---

# 9. Criando um Jogo (Exemplo: Quiz)

Arquivo: games/quiz.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function quiz() {

    const questions = [
        {
            question: "She ____ my friend.",
            options: ["1) am", "2) is", "3) are"],
            answer: "2"
        },
        {
            question: "They ____ students.",
            options: ["1) is", "2) are", "3) am"],
            answer: "2"
        }
    ];

    questions.forEach(q => {

        console.log("\n" + q.question);
        q.options.forEach(opt => console.log(opt));

        let answer = readline.question("Answer: ");

        if(answer === q.answer) {
            console.log("Correct!");
            gameState.addScore(10);
        } else {
            console.log("Wrong!");
            gameState.loseLife();
        }

    });

    readline.question("\nPress ENTER to continue...");
}

module.exports = quiz;
```

---

# 10. games/completeSentence.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function completeSentence() {

    const sentences = [
        { text: "I ____ a developer.", answer: "am" },
        { text: "She ____ coding now.", answer: "is" }
    ];

    sentences.forEach(s => {

        console.log("\nComplete:");
        console.log(s.text);

        let answer = readline.question("Word: ").toLowerCase();

        if(answer === s.answer) {
            console.log("Correct!");
            gameState.addScore(10);
        } else {
            console.log("Wrong! Correct answer:", s.answer);
            gameState.loseLife();
        }

    });

    readline.question("\nPress ENTER to continue...");
}

module.exports = completeSentence;
```

---

# 11. games/sentenceBuilder.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function sentenceBuilder() {

    const challenge = {
        words: ["developer", "is", "He", "a"],
        correct: "He is a developer"
    };

    console.log("\nReorder the words to form a sentence:");
    console.log(challenge.words.join(" | "));

    let answer = readline.question("Sentence: ");

    if(answer === challenge.correct) {
        console.log("Correct!");
        gameState.addScore(15);
    } else {
        console.log("Wrong! Correct sentence:", challenge.correct);
        gameState.loseLife();
    }

    readline.question("\nPress ENTER to continue...");
}

module.exports = sentenceBuilder;
```

---

# 12. games/memoryChallenge.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function memoryChallenge() {

    const words = ["code", "debug", "function", "variable"];

    console.log("\nMemorize these words:");
    console.log(words.join(", "));

    readline.question("\nPress ENTER when ready...");

    console.clear();

    let answer = readline.question("Type the words separated by comma: ");

    if(answer === words.join(", ")) {
        console.log("Perfect memory!");
        gameState.addScore(20);
    } else {
        console.log("Not quite!");
        gameState.loseLife();
    }

    readline.question("\nPress ENTER to continue...");
}

module.exports = memoryChallenge;
```

---

# 13. games/battleRPG.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function battleRPG() {

    let enemyHP = 30;

    console.log("\nA Grammar Monster appears!");

    while(enemyHP > 0) {

        console.log("\nEnemy HP:", enemyHP);
        console.log("Answer correctly to attack.");

        let answer = readline.question("Past of 'go': ");

        if(answer.toLowerCase() === "went") {
            console.log("Hit!");
            enemyHP -= 10;
            gameState.addScore(10);
        } else {
            console.log("Miss! You got hit.");
            gameState.loseLife();
            break;
        }
    }

    if(enemyHP <= 0) {
        console.log("Monster defeated!");
    }

    readline.question("\nPress ENTER to continue...");
}

module.exports = battleRPG;
```

---

# 14. games/detectiveStory.js

```js
const readline = require('readline-sync');
const gameState = require('../gameState');

function detectiveStory() {

    console.log("\nYou are a detective solving a mystery.");

    console.log("\nChoose the correct word:");
    console.log("The suspect ____ nervous.");

    console.log("1) look");
    console.log("2) looks");
    console.log("3) looking");

    let answer = readline.question("Option: ");

    if(answer === "2") {
        console.log("Clue discovered!");
        gameState.addScore(15);
    } else {
        console.log("Wrong clue!");
        gameState.loseLife();
    }

    readline.question("\nPress ENTER to continue...");
}

module.exports = detectiveStory;
```

---

# 15. Entendendo require e module.exports

Quando usamos:

```
const quiz = require('./games/quiz');
```

Estamos importando o que foi exportado com:

```
module.exports = quiz;
```

Isso permite dividir o projeto em partes independentes.

---

# Missão: Expansão Linguística Obrigatória

Cada aluno deve adicionar **no mínimo 2 questões para cada estrutura abaixo**.

---

# Estruturas Obrigatórias

## Presente Simples

Exemplo:

* She works every day.
* They play soccer.

---

## Passado Simples

Exemplo:

* I went to work yesterday.
* She fixed the bug.

---

## Negação no Presente

Exemplo:

* I don’t like bugs.
* She doesn’t understand.

---

## Negação no Passado

Exemplo:

* I didn’t push the code.
* They didn’t finish.

---

## Contrações

Exemplo:

* I am → I’m
* She is → She’s
* Do not → Don’t
* Did not → Didn’t

Pode ser:

* Complete a frase usando contração
* Transforme para forma contraída

---

## Verbo “to be”

* Afirmativa
* Negativa
* Interrogativa

---

## Perguntas com Do/Does

Exemplo:

* Do you code?
* Does she work here?

---

## Perguntas no Passado (Did)

Exemplo:

* Did you finish the task?

---

## Plural

* Variable / Variables
* Class / Classes

---

## There is / There are

---

# 📌 Regras Importantes

1. Cada pergunta deve ter:

   * Frase
   * Resposta correta
   * Explicação simples da regra

Se errar, o sistema deve mostrar:

Explanation: We use "does" because it is third person singular.

Isso é obrigatório.

---


# Depois, crie um novo jogo que deve:

- Transformar frase afirmativa em negativa
- Transformar afirmativa em pergunta
- Transformar frase longa em contraída

Exemplo:

> She is working.
> Resposta esperada:
> She isn’t working.

---
















