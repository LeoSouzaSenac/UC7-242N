# Projeto — English Story RPG

## Objetivo

Crie um jogo interativo em inglês utilizando **HTML, CSS e JavaScript**.

O jogador deverá acompanhar uma história e completar frases escolhendo palavras corretas entre diferentes opções. As escolhas devem alterar a narrativa, gerar feedback e pontuação.

O jogo deve funcionar como um pequeno RPG narrativo com capítulos.

---

# Requisitos do Projeto

## 1. Estrutura Geral

O jogo deve possuir:

* Tela principal com:

  * título do jogo
  * barra de progresso
  * pontuação (XP)
  * número do capítulo

* Área da história:

  * texto narrativo
  * lacunas para completar

* Área de escolhas:

  * botões com palavras/opções

* Feedback:

  * informar se a escolha foi correta ou incorreta
  * explicar rapidamente o motivo gramatical

* Tela final:

  * pontuação final
  * resumo da história criada pelo jogador
  * botão para reiniciar o jogo

---

# Tema da História

Você pode escolher qualquer tema, por exemplo:

* escola misteriosa
* aventura medieval
* exploração espacial
* investigação policial
* mundo pós-apocalíptico
* fantasia mágica
* viagem no tempo

Toda a narrativa deve estar em inglês.

---

# Funcionamento do Jogo

## Cada capítulo deve conter:

### 1. Texto com lacunas

Exemplo:

```text
Sarah was _____ when she _____ the strange noise.
```

---

### 2. Opções de resposta

Exemplo:

* studying
* sleeping
* heard
* hear

---

### 3. Correção automática

O jogo deve:

* verificar se a escolha está "mais correta"
* atualizar a pontuação
* mostrar feedback

Exemplo:

```text
Correct! "was studying" uses Present Continuous.
```

ou

```text
Incorrect. "hear" should be in the Simple Past: "heard".
```

---

# Sistema de Pontuação

Sugestão:

* resposta correta = +10 XP
* resposta incorreta = +3 XP

O jogador nunca deve ficar sem pontuar.

---

# Quantidade Mínima

O projeto deve possuir no mínimo:

* 5 capítulos
* 2 lacunas por capítulo
* 4 opções por pergunta
* sistema de pontuação
* tela final

---

# Desafios Extras (Opcional)

Se quiser deixar o projeto mais avançado:

* adicionar sons
* adicionar efeitos visuais
* mudar imagem/cenário conforme escolhas
* adicionar múltiplos finais
* criar sistema de vidas
* salvar progresso no LocalStorage
* adicionar personagens
* adicionar inventário

---

# Conteúdo de Inglês

O jogo deve trabalhar pelo menos 3 dos conteúdos gramaticais que já vimos:

Exemplos:

* Verb to be
* Present Continuous
* Simple Past
* Simple Present
* Future
* Modal Verbs

---

# Organização do Código

Separar o projeto em:

```text
/index.html
/style.css
/script.js
```

---

# Critérios de Avaliação

## Inglês

* uso correto da gramática
* coerência das frases
* qualidade do vocabulário

## Programação

* funcionamento do jogo
* organização do código
* uso correto de JavaScript
* manipulação do DOM
* criatividade

## Design

* aparência visual
* responsividade
* experiência do usuário

---

# Entrega

Enviar:

* pasta do projeto
* arquivos HTML, CSS e JS
* imagens utilizadas
* link do GitHub (opcional)

---

# Exemplo de Ideia

```text
Chapter 1 — The Haunted Library

"The librarian was _____ when the lights suddenly _____ off."

Opções:
- reading
- danced
- went
- go
```


