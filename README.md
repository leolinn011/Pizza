# Pizza
// A lista de pizzas e seus placeholders de ingredientes
const menuPizzas = [
  { nome: "MARGUERITA", ingredientes: "?¿ Ingredientes da MARGUERITA ?¿" },
  { nome: "MUÇARELA", ingredientes: "?¿ Ingredientes da MUÇARELA ?¿" },
  { nome: "MUÇARELA AO ALHO FRITO", ingredientes: "?¿ Ingredientes da MUÇARELA AO ALHO FRITO ?¿" },
  { nome: "FRANGO AO ALHO FRITO", ingredientes: "?¿ Ingredientes do FRANGO AO ALHO FRITO ?¿" },
  { nome: "FRANGO A JARDINEIRA", ingredientes: "?¿ Ingredientes do FRANGO A JARDINEIRA ?¿" },
  { nome: "CALABRESA SEM CEBOLA", ingredientes: "?¿ Ingredientes da CALABRESA SEM CEBOLA ?¿" },
  { nome: "CALABRESA COM MILHO", ingredientes: "?¿ Ingredientes da CALABRESA COM MILHO ?¿" },
  { nome: "PRESUNTO", ingredientes: "?¿ Ingredientes do PRESUNTO ?¿" },
  { nome: "PRESUNTO COM CHEDDAR", ingredientes: "?¿ Ingredientes do PRESUNTO COM CHEDDAR ?¿" },
  { nome: "PRESUNTO COM MILHO", ingredientes: "?¿ Ingredientes do PRESUNTO COM MILHO ?¿" },
  { nome: "ROMANA", ingredientes: "?¿ Ingredientes da ROMANA ?¿" },
  { nome: "CEBOLA NA MANTEIGA DE GARRAFA", ingredientes: "?¿ Ingredientes da CEBOLA NA MANTEIGA DE GARRAFA ?¿" },
  { nome: "MILHO", ingredientes: "?¿ Ingredientes do MILHO ?¿" },
  { nome: "DOIS QUEIJOS", ingredientes: "?¿ Ingredientes de DOIS QUEIJOS ?¿" },
  { nome: "MILHO COM CHEDDAR", ingredientes: "?¿ Ingredientes do MILHO COM CHEDDAR ?¿" },
  { nome: "FRANGO COM CHEDDAR", ingredientes: "?¿ Ingredientes do FRANGO COM CHEDDAR ?¿" },
  { nome: "PALMITO", ingredientes: "?¿ Ingredientes do PALMITO ?¿" },
  { nome: "BRÓCOLIS", ingredientes: "?¿ Ingredientes do BRÓCOLIS ?¿" },
  { nome: "FRANGO ACEBOLADO", ingredientes: "?¿ Ingredientes do FRANGO ACEBOLADO ?¿" },
  { nome: "NAPOLITANA", ingredientes: "?¿ Ingredientes da NAPOLITANA ?¿" },
  { nome: "MUÇARELA COM DORITOS", ingredientes: "?¿ Ingredientes da MUÇARELA COM DORITOS ?¿" },
  { nome: "LOMBO CANADENSE COM BARBECUE", ingredientes: "?¿ Ingredientes do LOMBO CANADENSE COM BARBECUE ?¿" },
  { nome: "LOMBO CANADENSE A JARDINEIRA", ingredientes: "?¿ Ingredientes do LOMBO CANADENSE A JARDINEIRA ?¿" },
  { nome: "FRANGO COM BARBECUE", ingredientes: "?¿ Ingredientes do FRANGO COM BARBECUE ?¿" },
  { nome: "PRESUNTO PICANTE", ingredientes: "?¿ Ingredientes do PRESUNTO PICANTE ?¿" },
  { nome: "BRÓCOLIS COM ALHO FRITO", ingredientes: "?¿ Ingredientes do BRÓCOLIS COM ALHO FRITO ?¿" },
  { nome: "JASON PICANTE", ingredientes: "?¿ Ingredientes do JASON PICANTE ?¿" },
];

// Variável para controlar qual tela está sendo exibida
let telaAtual = 'menu'; // 'menu' ou 'ingredientes'

// Variável para armazenar a pizza selecionada
let pizzaSelecionada = null;

// Dimensões
const MARGEM = 20;
const ALTURA_ITEM = 30;
const COLUNAS = 3; // Número de colunas para exibir o menu

function setup() {
  createCanvas(600, 800); // Tela grande para caber o menu
  textAlign(CENTER, CENTER);
  textSize(14);
}

function draw() {
  background(255, 240, 220); // Cor de fundo suave

  if (telaAtual === 'menu') {
    desenharMenu();
  } else if (telaAtual === 'ingredientes') {
    desenharIngredientes();
  }
}

// --- Funções de Desenho ---

function desenharMenu() {
  fill(0);
  textSize(24);
  textStyle(BOLD);
  text("Cardápio de Pizzas 🍕", width / 2, MARGEM * 2);

  textStyle(NORMAL);
  textSize(14);

  // Calcula a largura da coluna
  const larguraColuna = (width - MARGEM * (COLUNAS + 1)) / COLUNAS;

  menuPizzas.forEach((pizza, index) => {
    // Cálculo de posição para layout em colunas
    const num = index + 1; // Número da pizza (1 a 27)
    const linha = floor(index / COLUNAS);
    const coluna = index % COLUNAS;

    const x = MARGEM + coluna * (larguraColuna + MARGEM) + larguraColuna / 2;
    const y = MARGEM * 5 + linha * (ALTURA_ITEM + 10);

    // Cria a "área clicável" para visualização
    const xRect = x - larguraColuna / 2;
    const yRect = y - ALTURA_ITEM / 2;

    // Verifica se o mouse está sobre o item para dar destaque
    if (mouseX > xRect && mouseX < xRect + larguraColuna &&
      mouseY > yRect && mouseY < yRect + ALTURA_ITEM) {
      fill(255, 200, 100); // Cor de destaque (laranja claro)
      rect(xRect, yRect, larguraColuna, ALTURA_ITEM, 5); // Retângulo arredondado
      fill(0); // Texto preto
      textStyle(BOLD);
    } else {
      fill(220); // Cor de fundo (cinza claro)
      rect(xRect, yRect, larguraColuna, ALTURA_ITEM, 5);
      fill(50); // Texto cinza escuro
      textStyle(NORMAL);
    }

    // Desenha o texto do nome da pizza
    text(`${num}- ${pizza.nome}`, x, y);
  });
}

function desenharIngredientes() {
  fill(0);
  textSize(28);
  textStyle(BOLD);
  // Título da pizza selecionada
  text(pizzaSelecionada.nome, width / 2, MARGEM * 4);

  // Ingredientes Placeholder
  textSize(18);
  textStyle(NORMAL);
  fill(50);
  text("Ingredientes:", width / 2, height / 3);

  textSize(16);
  // Usa a função text() com quebra de linha
  textAlign(LEFT, TOP);
  text(pizzaSelecionada.ingredientes, MARGEM * 3, height / 3 + 30, width - MARGEM * 6, height / 2);
  textAlign(CENTER, CENTER); // Volta ao alinhamento central

  // Botão de voltar
  const botaoX = width / 2;
  const botaoY = height - MARGEM * 3;
  const botaoL = 150;
  const botaoA = 40;

  // Verifica se o mouse está sobre o botão de voltar
  if (mouseX > botaoX - botaoL / 2 && mouseX < botaoX + botaoL / 2 &&
    mouseY > botaoY - botaoA / 2 && mouseY < botaoY + botaoA / 2) {
    fill(150, 0, 0); // Cor de destaque (vermelho escuro)
    cursor(HAND);
  } else {
    fill(200, 0, 0); // Cor normal (vermelho)
    cursor(ARROW);
  }
  rect(botaoX - botaoL / 2, botaoY - botaoA / 2, botaoL, botaoA, 8);
  fill(255);
  textSize(16);
  text("<- Voltar ao Menu", botaoX, botaoY);
}

// --- Funções de Interação ---

function mousePressed() {
  if (telaAtual === 'menu') {
    handleMenuClick();
  } else if (telaAtual === 'ingredientes') {
    handleIngredientesClick();
  }
}

function handleMenuClick() {
  const larguraColuna = (width - MARGEM * (COLUNAS + 1)) / COLUNAS;

  menuPizzas.forEach((pizza, index) => {
    const linha = floor(index / COLUNAS);
    const coluna = index % COLUNAS;

    const x = MARGEM + coluna * (larguraColuna + MARGEM) + larguraColuna / 2;
    const y = MARGEM * 5 + linha * (ALTURA_ITEM + 10);

    const xRect = x - larguraColuna / 2;
    const yRect = y - ALTURA_ITEM / 2;

    // Checa se o clique ocorreu dentro da área deste item
    if (mouseX > xRect && mouseX < xRect + larguraColuna &&
      mouseY > yRect && mouseY < yRect + ALTURA_ITEM) {
      // Define a pizza selecionada e muda para a tela de ingredientes
      pizzaSelecionada = pizza;
      telaAtual = 'ingredientes';
    }
  });
}

function handleIngredientesClick() {
  // Coordenadas e dimensões do botão "Voltar ao Menu"
  const botaoX = width / 2;
  const botaoY = height - MARGEM * 3;
  const botaoL = 150;
  const botaoA = 40;

  const xRect = botaoX - botaoL / 2;
  const yRect = botaoY - botaoA / 2;

  // Checa se o clique ocorreu no botão de voltar
  if (mouseX > xRect && mouseX < xRect + botaoL &&
    mouseY > yRect && mouseY < yRect + botaoA) {
    telaAtual = 'menu'; // Volta para o menu
    pizzaSelecionada = null;
  }
}