# ✈️ AeroExplore 3D — OpenSky Flight

Simulador de voo em mundo aberto para o navegador, feito com **Three.js**.
O avião (um monomotor de asa alta inspirado no **Cessna 172**, com cockpit completo), o mapa de **32 × 32 km**, os rios, os lagos, as construções e as árvores foram **gerados no Blender** por scripts Python, salvos dentro de [`blender/aeroexplore.blend`](blender/aeroexplore.blend).

🎮 **Jogar:** <https://henri-rodrigues.github.io/aeroexplore-3d/>

## Como voar

1. Dê partida com **I** e acelere com **W** até 100%.
2. Mantenha a reta com o leme (**Q**/**E**). O motor puxa o nariz para a esquerda.
3. A ~55 kt puxe **↓** com suavidade (nariz a ~8°) e suba a ~75 kt.
4. Use o compensador (**PgUp**/**PgDn**) para não precisar segurar o manche.
5. No pouso: potência ~25–35%, flaps 30° (**F**), ~65 kt na final.
   - O **PAPI** (luzes ao lado da pista) mostra 2 brancas + 2 vermelhas quando você está na rampa certa.
   - Arredonde perto do chão e toque primeiro com as rodas principais.
6. Freie com **Espaço** até parar: aparece **POUSO BEM-SUCEDIDO!**

Objetivo: visitar os **10 aeródromos** do mapa, incluindo um no planalto, um na montanha, um no arquipélago e um na ilha do vulcão.

| Tecla | Ação |
|---|---|
| `W` / `S` | Manete de potência + / − (com 0%, `S` freia) |
| `↓` / `↑` | Profundor: ↓ puxa (nariz sobe) · ↑ empurra |
| `A` `D` / `←` `→` | Ailerons (inclinar as asas) |
| `Q` / `E` | Pedais do leme · bequilha no solo |
| `PgUp` / `PgDn` | Compensador do profundor |
| `F` / `G` | Flaps: baixar / recolher (0°, 10°, 20°, 30°) |
| `I` | Partida / corte do motor |
| `Espaço` · `B` | Freios · freio de estacionamento |
| `C` | Câmera: cockpit → perseguição → órbita |
| Botão direito do mouse | Olhar ao redor no cockpit / girar a órbita |
| `Z` · roda do mouse | Centralizar a vista · zoom |
| `M` | Manche no mouse |
| `K` | Leme automático em voo (coordena as curvas) |
| Gamepad | Analógicos = manche e leme · gatilhos = potência · D-pad = compensador |
| `N` · `U` | Zoom do mapa · esconder os painéis |
| `T` · `R` | Avançar 1 hora · reiniciar no último aeródromo |
| `O` · `P` · `H` | Som · pausa · ajuda |

## O que há de realista

- **Física de voo 6-DOF** com coeficientes aerodinâmicos e inércias de um C172:
  - sustentação e arrasto conforme o ângulo de ataque;
  - estol a ~50 kt, que cai para ~45 kt com flaps;
  - efeito solo;
  - estabilidade em arfagem, rolagem e guinada, e guinada adversa;
  - torque e fator-P do motor;
  - sopro da hélice no leme;
  - vento com rajadas;
  - densidade do ar que cai com a altitude.
- **Trem de pouso com molas e amortecedores**:
  - o avião assenta no chão e quica em pousos duros;
  - a bequilha é esterçável;
  - há freios e atrito diferente na pista e na grama;
  - o trem quebra em impactos fortes, e a hélice ou as asas podem bater no chão.
- **Limites estruturais**: excesso de G e a VNE (163 kt).
- **Cockpit 3D** com instrumentos funcionando:
  - velocímetro, horizonte artificial, altímetro de 3 ponteiros, coordenador de curva com bola, giro direcional, variômetro e tacômetro;
  - combustível, óleo e um ponteiro GPS para o próximo aeródromo;
  - rádios.
  - Manches, manete e compensador se movem com os comandos.
- **Mundo**:
  - relevo com erosão;
  - rios e lagos calculados por escoamento da água (hidrologia);
  - florestas, lavouras, vilas e neve nos picos;
  - ciclo dia/noite e sombras em tempo real;
  - terreno com níveis de detalhe (LOD).

## Estrutura

```
index.html              o jogo (HTML + CSS + JavaScript, Three.js via CDN)
assets/aircraft.glb     avião + cockpit (Blender)
assets/buildings.glb    hangar, torre, casas, árvores e biruta (Blender)
assets/water.glb        lagos e rios (Blender)
assets/terrain.png      altura do terreno em 16 bits (R/G) + floresta (B)
assets/water.png        nível dos lagos + plataformas dos aeródromos
assets/terrain_color.jpg  textura de cor do terreno (2048 × 2048)
assets/world.json       aeródromos, vilas, lagos e traçado dos rios
blender/aeroexplore.blend  arquivo do Blender com os scripts de geração (Text Editor)
```

Para regenerar algo no Blender, abra `blender/aeroexplore.blend`, vá ao **Text Editor** e rode os scripts na ordem:
- `01`–`05` para o avião;
- `10`–`17` para o terreno e a água;
- `20` para as construções.

## Rodar no computador

O jogo carrega arquivos da pasta `assets/`, então precisa de um servidor local (abrir o `index.html` direto do disco não funciona):

```bash
python -m http.server 8000
```

Depois abra <http://localhost:8000> no navegador. Precisa de internet para baixar o Three.js do CDN unpkg.com.

---

# 🚀 Publicar no GitHub Pages

## 1. Criar o repositório no GitHub

1. Em <https://github.com>, clique em **+ → New repository**.
2. Dê um nome (por exemplo `aeroexplore-3d`) e deixe como **Public**.
3. **Não** marque README, `.gitignore` nem licença.
4. Clique em **Create repository**.

## 2. Enviar o projeto com o Git

Abra o terminal na pasta do projeto. Se for a primeira vez que usa o Git neste computador, configure seu nome e e-mail:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

Depois rode os comandos abaixo, trocando `SEU-USUARIO` pelo seu usuário do GitHub:

```bash
git init
git add .
git commit -m "Primeira versão do AeroExplore 3D"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/aeroexplore-3d.git
git push -u origin main
```

## 3. Ativar o GitHub Pages

1. No repositório, vá em **Settings → Pages**.
2. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
3. Selecione `main` e `/ (root)` e clique em **Save**.
4. Em 1 ou 2 minutos o jogo estará em `https://SEU-USUARIO.github.io/aeroexplore-3d/`.

## Atualizar depois

```bash
git add .
git commit -m "Descreva a mudança"
git push
```
