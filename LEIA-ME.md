# Gêmeo Digital Smart 4.0 — versão WebXR (Meta Quest 3)

Laboratório de Virtualização de Processos Industriais · UniSENAI · Campus Santo Amaro

Aplicação web em three.js que roda no computador (mouse) e no **Meta Quest 3** em realidade virtual ou realidade mista (passthrough). Não precisa instalar nada no óculos: ela abre no **Meta Quest Browser**.

## Conteúdo da pasta

| Arquivo | Para quê |
|---|---|
| `index.html` | A aplicação completa (simulação, interface e WebXR) |
| `vendor/three/` | Biblioteca three.js r160 (licença MIT), embutida para não depender de CDN |
| `logo_unisenai.png` | Adesivo da UniSENAI no vidro do laboratório |
| `floor_vinil.jpg` | Textura do piso vinílico |
| `manifest.webmanifest`, `icon-192.png`, `icon-512.png` | Permitem instalar como app (PWA) no Quest |
| `.nojekyll` | Evita processamento extra no GitHub Pages |

## 1. Publicar (o óculos exige HTTPS)

O WebXR só funciona em endereços **https://** (ou `localhost`). Escolha uma opção:

### Opção A — Netlify Drop (mais rápido, sem conta de Git)
1. Acesse **app.netlify.com/drop** no computador.
2. Arraste a pasta inteira (descompactada) para a página.
3. Copie o endereço gerado (ex.: `https://nome-aleatorio.netlify.app`).

### Opção B — GitHub Pages
1. Crie um repositório público no GitHub (ex.: `smart40-xr`).
2. Envie **todo o conteúdo da pasta** para a raiz do repositório (botão *Add file → Upload files*).
3. Em *Settings → Pages*, escolha *Deploy from a branch*, branch `main`, pasta `/ (root)`, e salve.
4. Em 1 ou 2 minutos o endereço fica disponível: `https://SEU-USUARIO.github.io/smart40-xr/`.

### Opção C — Servidor do SENAI-SP
Copie a pasta para qualquer servidor web com HTTPS. Não precisa de back-end.

> Abrir o `index.html` com duplo clique **não funciona** (o navegador bloqueia módulos em `file://`). Para testar no computador, rode na pasta: `python -m http.server 8000` e abra `http://localhost:8000`.

## 2. Abrir no Meta Quest 3

1. No óculos, abra o **Meta Quest Browser** e digite o endereço publicado.
2. Na barra inferior aparecem os botões **Entrar em VR** e **Realidade mista**.
3. Na primeira vez, aceite a permissão de uso do espaço/rastreamento.
4. (Opcional) No menu do navegador, use *Adicionar à biblioteca / Instalar app* para criar um atalho.

Dica: antes de entrar, defina o limite (Guardian) com espaço livre de cerca de 2 × 2 m. A bancada aparece em escala real (3,05 m de comprimento), cerca de 1,7 m à sua frente.

## 3. Controles dentro do óculos

| Ação | Controles Touch Plus | Mãos (hand tracking) |
|---|---|---|
| Apontar | Raio verde saindo do controle | Raio saindo da mão |
| Selecionar bancada, bloco, porta ou botão de emergência | Gatilho | Pinça (indicador + polegar) |
| Usar o painel flutuante (Pausar, velocidade, Emergência/Rearmar, Novo pedido, Portas, Visão geral) | Apontar + gatilho | Apontar + pinça |
| Teletransporte (só em VR) | Apontar para o piso (aparece um anel verde) + gatilho | Apontar para o piso + pinça |
| Andar | Manche esquerdo | — |
| Girar 30° | Manche direito para os lados | — |
| Sair | Botão Meta | Gesto do menu do sistema |

O **painel flutuante** fica à esquerda da bancada e mostra os indicadores, o estado da bancada selecionada, os sinais de E/S do CLP (ou a tag RFID do bloco) e os botões de operação.

### Realidade mista
No modo **Realidade mista** a sala virtual some e a bancada aparece sobre o ambiente real (passthrough), em tamanho real. É ideal para posicionar o gêmeo digital ao lado da bancada física do laboratório. Nesse modo o teletransporte fica desligado; caminhe fisicamente em volta.

## 4. Desempenho
- No computador, o botão **Gráficos HD** liga oclusão de ambiente, brilho das luminárias, sombras em alta resolução e reflexos do próprio laboratório. Em máquinas mais fracas, clique para mudar para **Gráficos leves** (a escolha fica salva no navegador).
- Dentro do óculos a renderização é direta (sem pós-processamento), com renderização foveada e sombras em resolução reduzida (three.js r160).
- Se ficar pesado, use a velocidade 1× e feche outras abas do navegador do Quest.
- Os modelos 3D dos controles são baixados automaticamente do CDN público da Immersive Web (precisa de internet); sem internet, o raio de apontar continua funcionando.

## 5. Referências usadas na modelagem
- Manual XL4002 (Exsto/Exxer) — lista de peças: SMC LEFS16, LEYG16, LERH50K, MHZL2-16D, MY1B, ZPT25; SCHUNK Co-act EGH (garra colaborativa); câmera MVISIA.
- Universal Robots — parâmetros DH do UR3e.
- Guia do Educador XL4002 — projeto integrado (Loja → MES → Estoque → Processo → Montagem → Expedição).
