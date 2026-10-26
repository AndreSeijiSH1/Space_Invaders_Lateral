# 👾 Space Invaders Lateral

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

Jogo no estilo **Space Invaders**, feito em **JavaScript puro + HTML5 `<canvas>`**, com a nave à esquerda e os invasores avançando da direita para a esquerda. Projeto de grupo da NI1 de **Programação Orientada a Objetos** (turma 2 NAADS), com foco em classes, herança e polimorfismo.

## Sumário

- [Integrantes e contribuições](#integrantes-e-contribuições)
- [Conceitos de POO aplicados](#conceitos-de-poo-aplicados)
- [Instalação e execução](#instalação-e-execução)
- [Controles](#controles)
- [Regras do jogo](#regras-do-jogo)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Uso de IA](#uso-de-ia)
- [Créditos](#créditos)

## Integrantes e contribuições

Cada integrante criou ou corrigiu pelo menos uma parte do jogo, e todas as etapas foram documentadas em relatórios.

| Integrante | O que fez |
|---|---|
| **André Seiji Shiroma** | **Telas de início e de fim** (com botão de jogar de novo e pontuação final). **Versão lateral**: nave nos 4 sentidos, tela cheia e desenhos de texto girados com `Sprites.girar()`. **Sistema de 5 hordas** controlado por uma tabela. **Ajuste final da horda 5** (de 8 para 6 colunas). Relatório da comparação Claude × Gemini. |
| **Marcos Almeida Daloia** | **Escudos** (barreiras de blocos que se desgastam com os tiros). **Passo fixo de 60 atualizações por segundo**, que corrige o bug de o jogo ficar 2,4× mais rápido em monitor de 144 Hz. **Setas e escudos na versão lateral**: setas e WASD unificados, nave que não atravessa os escudos e tiros bloqueados pelos escudos. Análise e documentação da pausa, dos sprites, do som e da dificuldade. |
| **Clayton Santos Ferreira** | **Botão e tecla de pausa** (P/Esc), com tela de pausa. **Pixel art** dos invasores e da nave, com 2 quadros de animação. **Som e música** gerados no navegador com a Web Audio API, sem arquivos de áudio. |
| **Enzo Mancio** | **Correção de escudo e dano visual**: a nave pisca em vermelho ao ser atingida, os escudos ficaram mais afastados da nave e os tiros do jogador passam a atravessá-los, de modo que só os tiros inimigos os danificam. |

O histórico completo, com o zip de cada versão e o relatório de cada etapa, está no repositório do grupo:
https://github.com/2026-2-NADS2/Projeto13/tree/main/POO%20N1

## Conceitos de POO aplicados

| Conceito | Onde aparece no código |
|---|---|
| **Classes e objetos** | Cada elemento do jogo é uma classe: `Jogador`, `Projetil`, `Barreira`, `Inimigo`, `Tela`, `Som`, `Musica` e `Jogo`. |
| **Herança (2 níveis)** | `Entidade` → `Inimigo` → `InimigoBasico`, `InimigoRapido` e `InimigoAtirador`. `Jogador`, `Projetil` e `Barreira` também herdam de `Entidade`, que guarda posição, tamanho e colisão. |
| **Polimorfismo** | `mover()`, `tentarAtirar()` e `desenhar()` são sobrescritos nas subclasses. O `Jogo` chama o mesmo método em todos os inimigos da lista e cada tipo responde do seu jeito (só o atirador dispara). |
| **Encapsulamento** | `Tela` esconde o acesso aos elementos da página. `Barreira.receberDano()` e `Jogador.receberDano()` guardam a regra de dano, e o `Jogo` só avisa que houve um acerto. |
| **Membros estáticos** | `Jogo.HORDAS`, `Jogo.SETAS_PARA_WASD`, `Jogo.X_ESCUDOS`, `Jogador.DURACAO_DANO` e `Barreira.criarEscudo()`. |
| **Composição** | O `Jogo` tem uma `Tela`, um `Som` e uma `Musica`. A `Musica` usa o `Som`. |
| **Responsabilidade única** | `Jogo` cuida das regras, `Tela` das mensagens, `Som` e `Musica` do áudio, `Sprites` dos desenhos. |
| **Função como parâmetro** | O `Jogo` entrega `() => this.iniciar()` para a `Tela` chamar quando o botão é clicado. |

## Instalação e execução

Não precisa instalar nada nem usar servidor. Basta um navegador atualizado (Chrome, Edge ou Firefox).

1. Neste repositório, clique no arquivo **Space Invaders Lateral.zip** *(ajuste o nome se o seu arquivo for diferente)*.
2. Clique em **Download raw file** (ícone de seta para baixo, no canto direito da barra acima do arquivo).
3. Extraia o zip: botão direito → **Extrair tudo** (Windows) ou dois cliques (Mac). Abrir o `index.html` de dentro do zip não funciona.
4. Abra a pasta `space-invaders-lateral`. Ela contém o `index.html`, o `style.css` e a pasta `js`. Mantenha os três juntos.
5. Dê dois cliques em **`index.html`**. O jogo abre no navegador. Clique em **Iniciar jogo** ou aperte **Enter**.

> As pastas `antes`, `prints` e `prints_novos` do zip são da documentação e não são necessárias para jogar.

**Alternativa com o VS Code:** abra a pasta extraída, clique com o botão direito em `index.html` e escolha **Open with Live Server**.

### Problemas comuns

| Problema | O que fazer |
|---|---|
| Tela em branco | Confira se a pasta `js` está ao lado do `index.html` e se o zip foi extraído de verdade. |
| Sem som | O navegador só libera o áudio depois de um clique ou tecla. Clique no jogo, aperte Enter e use **M** (som) e **N** (música). Se o botão mostrar "Som bloqueado", clique nele. |
| Jogo cortado na tela | Aperte **F** para tela cheia ou use o zoom do navegador (Ctrl e -). |

## Controles

| Tecla | Ação |
|---|---|
| Setas ou **W A S D** | Mover a nave nos 4 sentidos |
| **Espaço** | Atirar |
| **P** ou **Esc** | Pausar e continuar |
| **M** | Liga/desliga o som |
| **N** | Liga/desliga a música |
| **F** | Tela cheia |
| **Enter** | Iniciar ou jogar novamente |

## Regras do jogo

- Os invasores ficam em colunas, sobem e descem e, ao bater na borda, **avançam para a esquerda**.
- **Derrota:** perder as 3 vidas ou algum invasor chegar à borda esquerda.
- **Vitória:** eliminar todas as **5 hordas**.
- A cada horda as **vidas voltam para 3**, mas os **escudos continuam danificados** e a **pontuação acumula**.
- Os **escudos** bloqueiam os tiros dos invasores (aguentam 3 acertos e escurecem a cada dano). Os tiros da sua nave atravessam os escudos, e a nave não consegue atravessar os escudos.
- Ao ser atingida, a nave **pisca em vermelho** por cerca de 0,8 segundo.
- O jogo roda com **passo fixo de 60 atualizações por segundo**, então a velocidade é a mesma em qualquer monitor.

| Invasor | Pontos | Comportamento |
|---|---|---|
| Básico | 10 | Só se move |
| Rápido | 20 | Move-se mais depressa |
| Atirador | 30 | Dispara contra o jogador |

| Horda | Colunas | Invasores | Atiradores |
|---|---|---|---|
| 1 | 4 | 32 | 16 |
| 2 | 5 | 40 | 24 |
| 3 | 6 | 48 | 32 |
| 4 | 7 | 56 | 40 |
| 5 | 6 (10 por coluna) | 60 | 40 |

## Estrutura do projeto

```
index.html        Página, canvas, HUD e tela por cima (overlay)
style.css         Estilo e layout responsivo
js/
  Entidade.js         Classe base: posição, tamanho, desenhar() e mover()
  Jogador.js          Nave do jogador (4 eixos, vidas, tiro, receberDano())
  Projetil.js         Tiros do jogador e dos inimigos
  Barreira.js         Escudos (3 acertos; Barreira.criarEscudo())
  Inimigo.js          Classe base dos invasores
  InimigoBasico.js    Invasor básico (10 pts)
  InimigoRapido.js    Invasor rápido (20 pts)
  InimigoAtirador.js  Invasor que atira (30 pts)
  Sprites.js          Pixel art em mapas de texto, com 2 quadros de animação
  Tela.js             Tela de início, pausa, aviso de horda e fim de jogo
  Jogo.js             Laço principal, regras, colisões e tabela de hordas
  Som.js              Efeitos sonoros (Web Audio API)
  Musica.js           Música de fundo em loop (Web Audio API)
```

As tags `<script>` do `index.html` seguem a ordem das dependências (não usa módulos ES).

## Uso de IA

Foram usados **Gemini** e **Claude** na primeira versão do jogo, e os resultados foram comparados. O Gemini gerou uma versão muito simples (sem tiros inimigos, vidas, pontuação, derrota ou vitória). O Claude entregou uma base mais completa e organizada, com 3 tipos de inimigo e herança em dois níveis. Com a concordância do professor, o grupo seguiu **só com o Claude** nas melhorias seguintes. Todo o código foi revisado e testado pelo grupo.

## Créditos

- Jogo original **Space Invaders** (Taito, 1978), usado apenas como inspiração de jogabilidade.
- *Fix Your Timestep!*, de Glenn Fiedler: referência para o laço de passo fixo.
- Documentação da **Web Audio API** (MDN Web Docs): referência para sons e música.
- Código gerado e revisado com **Claude** (Anthropic) e **Gemini** (Google).
- Editado com **VS Code** + extensão **Live Server**.
- Nenhuma imagem, som ou biblioteca de terceiros: os sprites são mapas de texto e os sons são sintetizados no código.
