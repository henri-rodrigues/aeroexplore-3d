# ✈️ AeroExplore 3D — OpenSky Flight

Simulador arcade de voo em mundo aberto, feito com **Three.js** em um único arquivo `index.html`.
Ligue o motor, decole, explore montanhas, vales, rios, lagos e ilhas e pouse nos **6 aeródromos** do mapa.

## Como jogar

1. Dê partida no motor com **I**.
2. Acelere com **W** até ~65 kt e puxe **↓** para decolar. Ao soltar o manche, o avião segue subindo.
3. Siga os **feixes de luz âmbar**, a bússola (topo da tela) e o minimapa até um aeródromo.
4. Para pousar: flaps (**F**) em 2, ~70 kt, asas niveladas e uma descida suave. As luzes **PAPI** ao lado da pista indicam a rampa: 2 brancas + 2 vermelhas significa que você está na rampa certa.
5. Freie com **Espaço** até parar. Aparece **POUSO BEM-SUCEDIDO!** e o aeródromo vira seu ponto de reinício.

| Tecla | Ação |
|---|---|
| `W` / `S` | Potência do motor + / − (com 0%, `S` freia) |
| `↓` / `↑` | Arfagem: ↓ puxa o manche (sobe) · ↑ empurra (desce) |
| `A` `D` / `←` `→` | Rolagem (inclinar as asas) · direção no solo |
| `Q` / `E` | Leme (guinada), para alinhar com a pista |
| `I` | Ligar / desligar o motor |
| `F` | Flaps 0 → 1 → 2 |
| `Espaço` | Freios |
| `C` | Câmera 3ª pessoa / cockpit |
| `M` | Pilotar com o mouse (liga/desliga) |
| Roda do mouse | Distância da câmera |
| `N` | Zoom do minimapa |
| `T` | Avançar 1 hora (ciclo dia/noite) |
| `R` | Reiniciar no último aeródromo |
| `V` · `P` · `H` | Som · Pausa · Ajuda |

> **Observação:** no pedido original, `W`/`S` serviam tanto para o acelerador quanto para a arfagem. Para não haver conflito, `W`/`S` controlam o **acelerador** e as **setas ↑/↓** (ou o mouse) controlam a **arfagem**.

## Recursos

- Terreno procedural de 12 × 12 km (sempre o mesmo mapa): montanhas com neve, vales, rios, lagos, ilhas e oceano.
- 6 aeródromos posicionados automaticamente em terreno plano e com a rampa de aproximação livre de morros.
- Pistas com marcações reais (cabeceiras, números, eixo e zona de toque), luzes de borda e PAPI, hangares, torre de controle e biruta.
- Céu com ciclo dia/noite, sol dinâmico, estrelas, névoa de distância, sombras em tempo real e água com reflexo, ondas e transparência.
- Física arcade: sustentação proporcional à velocidade², estol abaixo de ~58 kt (sem flaps), proteção contra estol e avaliação do pouso (razão de descida, asas niveladas, velocidade e local do toque).
- HUD com velocímetro (kt e km/h), horizonte artificial, altímetro (pés e metros), variômetro, potência, bússola e minimapa.
- Sons sintetizados (motor, vento, alarme de estol) e qualidade adaptativa para manter ~60 FPS.

## Rodar no computador

Dê dois cliques em `index.html` (precisa de internet, porque o Three.js vem do CDN unpkg.com).

---

# 🚀 Guia: publicar no GitHub Pages

## 1. Criar o repositório no GitHub

1. Entre em <https://github.com> e faça login (ou crie uma conta gratuita).
2. Clique no **+** no canto superior direito → **New repository**.
3. Em **Repository name**, digite por exemplo `aeroexplore-3d`.
4. Deixe como **Public**. O GitHub Pages gratuito exige repositório público.
5. **Não** marque “Add a README file”, nem `.gitignore` ou licença. O repositório precisa começar vazio.
6. Clique em **Create repository** e deixe a página aberta. Ela mostra o endereço do repositório, algo como
   `https://github.com/SEU-USUARIO/aeroexplore-3d.git`.

## 2. Enviar o projeto com o Git

Abra o terminal **dentro da pasta do projeto**. No Windows: abra a pasta no Explorador de Arquivos, clique com o botão direito num espaço vazio e escolha **Abrir no Terminal** (ou **Git Bash Here**).

Na primeira vez que usar o Git neste computador, configure seu nome e e-mail:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

Depois rode, um de cada vez:

```bash
git init
git add .
git commit -m "Primeira versão do AeroExplore 3D"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/aeroexplore-3d.git
git push -u origin main
```

O que cada um faz:

| Comando | O que faz |
|---|---|
| `git init` | Transforma a pasta em um repositório Git |
| `git add .` | Marca todos os arquivos (`index.html`, `README.md`) para o próximo commit |
| `git commit -m "..."` | Salva uma “foto” dos arquivos com uma mensagem |
| `git branch -M main` | Dá o nome `main` ao ramo principal |
| `git remote add origin ...` | Liga a pasta local ao repositório do GitHub (troque `SEU-USUARIO`) |
| `git push -u origin main` | Envia os arquivos para o GitHub |

No primeiro `git push`, o Windows abre uma janela de login do GitHub. Basta autorizar no navegador.

## 3. Ativar o GitHub Pages

1. No repositório do GitHub, clique em **Settings** (Configurações).
2. No menu lateral, clique em **Pages**.
3. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
4. Em **Branch**, selecione `main` e a pasta `/ (root)`, e clique em **Save**.
5. Aguarde de 1 a 2 minutos e atualize a página. Vai aparecer: **“Your site is live at”**
   `https://SEU-USUARIO.github.io/aeroexplore-3d/`

Esse é o link público do jogo. Qualquer pessoa pode abri-lo no navegador do computador.

## Atualizar o jogo depois

Sempre que alterar o `index.html`:

```bash
git add .
git commit -m "Descreva a mudança"
git push
```

Em 1 ou 2 minutos o GitHub Pages publica a nova versão no mesmo link.
