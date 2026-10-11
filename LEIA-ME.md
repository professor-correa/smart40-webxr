# Gêmeo Digital Smart 4.0 — versão WebXR (Meta Quest 3)

Laboratório de Virtualização de Processos Industriais · UniSENAI · Campus Santo Amaro

Aplicação web em three.js que roda no computador (mouse) e no **Meta Quest 3** em realidade virtual ou realidade mista (passthrough). Não precisa instalar nada no óculos: ela abre no **Meta Quest Browser**.

## Conteúdo da pasta

| Arquivo | Para quê |
|---|---|
| `index.html` | A aplicação completa (simulação, interface e WebXR) |
| `vendor/three/` | Biblioteca three.js r160 (licença MIT), embutida para não depender de CDN |
| `models/ur3e.glb` | Robô UR3e, convertido do STEP oficial da Universal Robots (peça 1006926): um nó por elo, articulado nas juntas da cena |
| `models/egh80.glb` | Garra SCHUNK Co-act EGH 80-IOL-N-UREK, convertida do STEP do fabricante (CADENAS, licença CC BY-ND 4.0) |
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
| Usar o painel flutuante (Pausar, velocidade, Emergência/Rearmar, Loja, Portas, Visão geral) | Apontar + gatilho | Apontar + pinça |
| Teletransporte (só em VR) | Apontar para o piso (aparece um anel verde) + gatilho | Apontar para o piso + pinça |
| Andar | Manche esquerdo | — |
| Girar 30° | Manche direito para os lados | — |
| Sair | Botão Meta | Gesto do menu do sistema |

Com o rastreamento de mãos, as mãos aparecem como uma malha articulada com tom de pele (modelo genérico do WebXR, baixado da internet na primeira vez). Sem internet, voltam a ser esferas nas articulações.

O **painel flutuante** fica à esquerda da bancada e mostra os indicadores, o estado da bancada selecionada, os sinais de E/S do CLP (ou a tag RFID do bloco) e os botões de operação.

### Fazer um pedido na loja (dentro do óculos)
No painel flutuante, toque em **Loja**. A página de personalização é a mesma da loja no computador:
1. Escolha o número de **andares** (1, 2 ou 3).
2. Aponte para o **bloco** ou para uma **lâmina** (esquerda, frontal, direita) de um andar; embaixo aparecem as cores e, para lâminas, os desenhos (casa, barco, estrela).
3. Toque em **Gerar pedido**: a OP entra no MES e a mensagem de confirmação aparece no painel. **Aleatório** sorteia uma nova combinação e **Voltar** retorna ao painel de operação.

O botão **Pedidos automáticos** liga ou desliga os pedidos gerados pela loja virtual. As escolhas feitas no óculos e no formulário do computador são as mesmas.

### Realidade mista
No modo **Realidade mista** a sala virtual some e a bancada aparece sobre o ambiente real (passthrough), em tamanho real. É ideal para posicionar o gêmeo digital ao lado da bancada física do laboratório. Nesse modo o teletransporte fica desligado; caminhe fisicamente em volta.

## 4. Supervisório da planta (SCADA)

Clique na **tela do notebook** da bancada 5 · Integração. A tela do notebook já mostra uma miniatura do supervisório ao vivo.

- **No computador:** a câmera flutua até o notebook e a tela se expande para a janela inteira. Para sair, use **Fechar**, a tecla **Esc** ou clique fora da tela. A câmera volta ao ponto de onde saiu.
- **Em VR:** aponte para a tela do notebook e aperte o gatilho (ou faça a pinça). Você flutua até a frente do notebook e o supervisório abre como um painel grande. Aponte para os botões do painel para navegar.
- **Em realidade mista:** o painel abre à sua frente, sem mover você, para não desalinhar a bancada virtual da real.

| Aba | O que mostra |
|---|---|
| Visão geral | OEE (disponibilidade, desempenho, qualidade), indicadores e sinótico da linha com estado das bancadas, blocos na esteira e torre de sinalização |
| Produção · MES | Ordens com etapa e lead time, ordens por etapa, gráfico de lead time e comandos da loja |
| Sensores | Tags de campo com valor, faixa, estado e tendência de 3 min: pressão pneumática, vácuo, temperatura dos drives, vibração dos motores, potência, compressor e vazão de ar |
| Posicionamento | Eixos e drives de cada bancada, incluindo as juntas do UR3e: posição, curso, velocidade e erro de seguimento |
| Energia | Potência e energia, Wh por OP, custo, emissões, energia em espera, ar comprimido e ciclos de válvulas |
| Qualidade | Inspeções da câmera MVISIA por cor, FPY e carta de controle (CEP) do encaixe das lâminas com Cp/Cpk |
| Manutenção | Horas, ciclos, zona de vibração ISO 10816 e saúde dos ativos. O rolamento do motor da esteira da montagem se desgasta com o uso; quando entra na zona C, registre a manutenção |
| Alarmes | Alarmes ativos por prioridade, reconhecimento pelo operador e histórico de eventos |

Os dados são simulados a partir do estado real do gêmeo digital (saídas dos CLPs, eixos, esteira, OPs e inspeções).

## 5. Sala de aula

O laboratório está montado como sala de aula, a partir de fotos do espaço real:
- **6 postos de trabalho**, 3 de cada lado da célula, com os alunos voltados para a lousa. Cada posto tem uma mesa com tampo preto e borda de compensado aparente, estrutura em tubo de aço com rodízios, gabinete Dell em torre, monitor Dell 24" com webcam, teclado, mouse e cadeira giratória de tela.
- **Mesa do professor** na frente da sala, de frente para a turma.
- **Lousa de vidro** na parede oposta à divisória da célula, com o fluxo da OP e as anotações da aula.

## 6. Bancadas (gabinete Smart 4.0)

Modelagem a partir do manual e das fotos da bancada (detalhada primeiro na **Estoque**):
- **Gabinete:** laterais em moldura arredondada com painel rebaixado, frente preta e porta com os decalques da bancada (cubo SMART 4.0, nome na vertical, SENAI+digital e filete verde). Clique na porta, ou use o botão **Portas**, para abrir.
- **Painel de botões da IHM** (desenho de conjunto e lista de materiais): perfil de alumínio anodizado 115 × 185 mm cortado em 400 mm, laterais pintadas com 8 parafusos, chapa frontal de 4 mm com legendas e logotipo, IHM KTP700 Basic em tamanho real (moldura com SIEMENS, SIMATIC HMI, TOUCH e teclas F1–F8), comutador SETUP, botões START e STOP, botão luminoso RESET, sinaleiros SEGURANÇA OK e SEGURANÇA ACIONADA e botão soco Ø40 sobre a plaqueta EMERGÊNCIA / DESLIGA. Os sinaleiros e o RESET acompanham a emergência, e cada item mostra o código da lista de materiais ao ser clicado.
- **Painel elétrico** (atrás da porta): placa de montagem com 3 trilhos DIN e canaletas. Trilho superior: multimedidor Smart Sense, fonte SITOP 24 Vcc, client Wi-Fi e drives dos atuadores elétricos. Trilho do meio: CLP, switch Ethernet de 5 portas, distribuidor 24 Vcc e relé de segurança. Trilho inferior: disjuntores, relés de interface e contatores.
- **Compartimento traseiro:** filtro regulador, válvula de bloqueio, válvulas, gerador de vácuo, vacuostato e régua com entrada e saída de ar, válvula manual, alimentação, seccionadora geral, tomada da próxima bancada e porta RJ-45.
- **Estoque:** magazine com 5 bandejas em arco (35 posições), alojamentos com insertos e colunas com espaçadores; caixa de conexão elétrica das esteiras. O manipulador é uma cadeia montada peça sobre peça: atuador elétrico de giro (LERH50K) no tampo → atuador linear vertical (LEFS16B-250, motor em cima, esteira porta-cabos que acompanha o carro) → cilindro posicionador horizontal preso ao carro → garra MHZL2-16D. O curso de 250 mm vai da esteira ao nível superior do magazine.

- **Processo:** pórtico com 3 colunas de perfil 40×40 e cantoneiras, chapa de aço sob o eixo X. Cadeia montada peça sobre peça: eixo X (LEFS16RB-400, motor paralelo, porta-cabos em calha) → eixo Y (LEYG16MB-150 parafusado no carro X, porta-cabos com curva na ponta fixa) → eixo Z pneumático (cilindro com 2 hastes-guia sobre suporte com adesivo de alerta, prolongador e ventosa). Magazine com dedos em perfil L, base para gravação em pedestal, depósito serrilhado para o robô e passa-cabos no tampo. Compartimento traseiro com 2 geradores de vácuo.

- **Montagem:** magazine de tampa e base de montagem elevado sobre 2 colunas (chapa preta com 3 janelas e tubo de acrílico na ponta), rampa alimentadora de Smart Block inclinada na lateral esquerda, base de translado com moldura preta sobre colunas, sistema de visão no alto da coluna e teach pendant UR e-Series (moldura azul) à direita do console. Painel elétrico com o layout do manual 7.3.3 (CLP e interface IO-Link da garra no trilho de cima), mantendo o CLP **S7-1500** da bancada real (CPU 1511C com display, teclado e conectores frontais, 3 módulos de sinais e módulo azul). As demais bancadas usam o S7-1200 (CPU 1214C). Compartimento traseiro conforme 7.3.2: bloco de válvulas branco, vacuostato digital e passagens laterais (item 13).

- **Expedição** (subconjuntos 102461 e 102462): prateleira de produtos finalizados com 2 colunas de perfil 30×30 × 445 mm e 3 bandejas numeradas de 1 a 12 (chapa cinza e pente preto). Manipulador montado peça sobre peça: eixo X LEFS16RB-400 com guia linear OBR-B-15R, proteção em acrílico e porta-cabos → espaçador de união dos patins → giro LERH50K com proteção em acrílico → disco de união, base e mão-francesa → eixo vertical LEFS16B-300 com porta-cabos → suporte em ponte → base plana transportadora com cilindro pneumático D10×100 (válvulas de fluxo e sensores) e ventosa ZPT25. Compartimento traseiro com tomada redonda para a próxima bancada e placas de aviso de eletricidade e risco pneumático.

- **Robô e garra da Montagem:** geometria real dos arquivos STEP do fabricante, convertida para GLB com o gmsh (malha simplificada para rodar no Quest). As tampas azuis do UR3e são identificadas pela geometria, nas pontas dos eixos das juntas. Cores do UR3e conforme o desenho de conjunto: carcaças cinza-escuras, tubos claros com anéis pretos, tampas ciano e base cinza-azulada. Os dedos seguem o kit Starter da SCHUNK (≈ 90 mm × 29 mm, presos ao bloco de fixação dos mordentes): corpo branco curvo, faixa cinza nervurada e pastilha de borracha envolvendo a ponta. Se os arquivos GLB não carregarem, a cena usa os modelos procedurais.

**Portas e identificação de componentes**
- Todas as bancadas têm porta frontal (painel elétrico) e porta metálica traseira (compartimento pneumático). Clique para abrir: no computador a câmera se aproxima de frente para o painel; clique de novo para fechar e voltar à vista anterior. As duas portas da Montagem abrem juntas.
- Com a porta aberta, clique em um componente: aparece um cartão com o número do item no manual, o nome e a função, e a peça fica contornada em verde. Esc, clicar fora ou girar a câmera fecha o cartão. No óculos, o componente apontado aparece no painel flutuante.

As demais bancadas já usam o mesmo gabinete e console; o conteúdo do painel delas segue o layout da Estoque até receberem o detalhamento próprio.

## 7. Teach pendant do UR3e (operação e programação)

O robô da Montagem tem um teach pendant UR e-Series com a interface PolyScope simulada, seguindo o Guia do Educador XL4002 (p. 272–295) e o Manual do Usuário UR3e (cap. 3.2.3, 7.4, 7.7 e 11). O pendant 3D fica pendurado na frente da bancada da Montagem (moldura azul, parada de emergência, botão liga/desliga, porta USB, botão Freedrive na traseira e cabo até a caixa de controle) e mostra a tela ao vivo.

**Abrir**
- **No computador:** clique no pendant na bancada ou no botão **Teach pendant** da barra inferior. O pendant abre ao lado da cena, com o robô à vista à esquerda e o roteiro de aprendizagem no alto. **Devolver ao suporte** ou Esc fecha.
- **No óculos:** aproxime qualquer mão do pendant e aperte o **botão de pega** (ou aponte para ele e aperte o gatilho). O pendant fica preso à **mão esquerda**, logo acima da palma e com a tela voltada para o seu rosto; a mão direita toca a tela.

| Ação no óculos | Controles Touch Plus | Mãos (hand tracking) |
|---|---|---|
| Pegar o pendant (vai para a mão esquerda) | Botão de pega perto dele, ou raio + gatilho | Pinça perto do pendant |
| Tocar a tela | Raio da mão direita + gatilho | Encostar a ponta do indicador direito na tela |
| Freedrive (botão traseiro) | Segurar o **gatilho esquerdo** | Pinça da mão esquerda, ou botão Freedrive da tela |
| Conduzir o robô em Freedrive | Com o Freedrive ativo, botão de pega da mão direita perto da ferramenta e mover a mão | Pinça da direita perto da ferramenta e mover a mão |
| Pegar a peça de treino com a mão | Botão de pega perto do bloco azul | Pinça perto do bloco |
| Guardar o pendant | Encostar o pendant no suporte, **Devolver pendant** no painel do roteiro ou menu ☰ → Guardar pendant no suporte | Igual |

**Telas do PolyScope**
- **Cabeçalho:** abas Executar, Programa, Instalação, Mover, E/S e Registro; programa e instalação ativos; Novo, Abrir e Salvar; modo **Remoto/Local**; soma de verificação de segurança; menu (Ajuda, Sobre, **idioma português/inglês** e Desligar robô).
- **Rodapé:** botão de estado do robô (Desligado, Inativo, Normal), velocidade, ▶ executar/pausar, passo a passo, ■ parar e Simulação.
- **Inicializar:** LIGAR → Inativo (amarelo) → INICIAR libera os freios (pequeno tranco) → Normal (verde) → Sair.
- **Mover:** setas de posição do TCP (linear) e de orientação (giro em torno do TCP) no recurso Visão, Base ou Ferramenta; setas de cada junta; posição da ferramenta (toque num valor para digitar a pose e mover o robô até ela); Início (Home), Alinhar, Freedrive (Todos livres, Plano, Transladar, Rotação) e a barra do URCap da garra EGH (Abrir/Fechar).
- **Programa:** comandos Básico (Mover, Ponto de passagem, Esperar, Definir, Popup, Parar, Comentário, Pasta), Avançado (Loop) e URCaps (Garra EGH); árvore com &lt;vazio&gt;, nós em amarelo quando incompletos e seta azul no nó em execução; barra ▲ ▼ Copiar Colar Excluir; painéis Comando, Gráficos e Variáveis. O Mover tem MoveJ, MoveL e MoveP com velocidade e aceleração (teclado numérico como no guia). O ponto de passagem é gravado com **Definir ponto de passagem → mover o robô → OK** e tem **Mover aqui**.
- **Executar:** ao tocar ▶, a tela **Mover robô para posição** pede para segurar **Automático** até o robô chegar ao primeiro ponto; depois o programa roda sozinho. Movimento linear impossível ou TCP abaixo do tampo da bancada geram parada de proteção.
- **Instalação:** TCP (centro da flange ou TCP da garra EGH), Montagem, Carga útil, Posição inicial (Home), Fieldbus PROFINET e limites de segurança.
- **E/S:** entradas e saídas configuráveis e digitais (toque nas entradas para simular o sinal do CLP), analógicas e da ferramenta. **Registro:** leituras, carga nas juntas e registro de eventos.

**Controle Local e Remoto**
Em **Remoto**, o CLP S7-1500 comanda o robô pelo PROFINET e a Montagem roda o ciclo automático. Ao tocar no ícone **Remoto** e escolher **Controle local**, o ciclo automático congela onde está, e aparecem na bancada a **peça de treino** (bloco azul) no **ponto A** (laranja) e o **ponto B** (verde). Para devolver, toque em **Local → Remoto** e segure **Automático**: o robô volta à pose em que o ciclo parou, a peça de treino sai e a Montagem retoma os pedidos. A emergência no controle local desliga o braço e exige nova inicialização.

**Roteiro de aprendizagem** (painel ao lado do pendant; no óculos, painel flutuante ao lado do robô). Cada passo é conferido automaticamente e o botão a tocar pisca em laranja na tela do pendant:
1. Ligar o robô e assumir o controle (Guia p. 278)
2. Mover o robô: setas, juntas, Freedrive e Home (p. 279)
3. Instalação: TCP, carga útil e Home (p. 280–282)
4. Primeiro programa: Move e Waypoints, MoveJ × MoveL (p. 283–286)
5. Experiência 1: pegar a peça em A e entregar em B com a garra EGH (p. 287). O programa pronto está em **Abrir… → exemplo_pega_e_coloca**.
6. Lógica: Loop, Esperar entrada digital, Definir saída e a aba E/S (p. 283–284 e 294)
7. Devolver o robô ao CLP (Remoto) e o PROFINET (p. 289–295)

Os programas salvos (**Salvar…**) ficam no navegador de cada computador ou óculos.

## 8. Desempenho
- No computador, o botão **Gráficos HD** liga oclusão de ambiente, brilho das luminárias, sombras em alta resolução e reflexos do próprio laboratório. Em máquinas mais fracas, clique para mudar para **Gráficos leves** (a escolha fica salva no navegador).
- Dentro do óculos a renderização é direta (sem pós-processamento), com renderização foveada e sombras em resolução reduzida (three.js r160).
- Se ficar pesado, use a velocidade 1× e feche outras abas do navegador do Quest.
- Os modelos 3D dos controles são baixados automaticamente do CDN público da Immersive Web (precisa de internet); sem internet, o raio de apontar continua funcionando.

## 9. Referências usadas na modelagem
- Manual XL4002 (Exsto/Exxer) — lista de peças: SMC LEFS16, LEYG16, LERH50K, MHZL2-16D, MY1B, ZPT25; SCHUNK Co-act EGH (garra colaborativa); câmera MVISIA.
- Universal Robots — parâmetros DH do UR3e; Manual do Usuário UR3e (710-954-00): Teach Pendant, PolyScope, inicialização, Freedrive e programação.
- Guia do Educador XL4002 — projeto integrado (Loja → MES → Estoque → Processo → Montagem → Expedição).
- Guia do Educador XL4002, p. 272–295 — robô colaborativo UR E3: Teach Pendant, telas do PolyScope, TCP, carga útil, comandos Basic/Advanced/Templates, MoveJ/L/P, experiências e integração com o CLP por PROFINET.
