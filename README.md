// A lista de pizzas ATUALIZADA e seus placeholders de ingredientes
const menuPizzas = [
  
  // ===================================
  // ## PIZZA SALGADA (1 - 20)
  // ===================================
  
  // 1- MARGUERITA
  { nome: "MARGUERITA", ingredientes: "Molho de tomate, muçarela, rodelas de tomate, manjericão e azeite extra virgem" },
  // 2- MUÇARELA
  { nome: "MUÇARELA", ingredientes: "Molho de tomate e farta camada de muçarela" },
  // 3- CALABRESA COM MUÇARELA 
  { nome: "CALABRESA COM MUÇARELA", ingredientes: "Molho de tomate, linguiça calabresa fatiada e muçarela" },
  // 4- RÚCULA 
  { nome: "RÚCULA", ingredientes: "Molho de tomate, muçarela, tomate seco e folhas frescas de rúcula" },
  // 5- FRANGO A JARDINEIRA
  { nome: "FRANGO A JARDINEIRA", ingredientes: "Molho de tomate, muçarela, frango desfiado, milho, ervilha, palmito e azeitonas" },
  // 6- CINCO QUEIJOS 
  { nome: "CINCO QUEIJOS", ingredientes: "Molho de tomate, muçarela, provolone, parmesão, gorgonzola e catupiry" },
  // 7- PEPERONE 
  { nome: "PEPERONE", ingredientes: "Molho de tomate, muçarela e fatias generosas de peperone" },
  // 8- PORTUGUESA 
  { nome: "PORTUGUESA", ingredientes: "Molho de tomate, muçarela, presunto, ovos cozidos, cebola e azeitonas pretas" },
  // 9- BATATA FRITA 
  { nome: "BATATA FRITA", ingredientes: "Molho de tomate, muçarela, bacon em cubos e batatas fritas cobertas com cheddar cremoso" },
  // 10- PRESUNTO PARMA
  { nome: "PRESUNTO PARMA", ingredientes: "Molho de tomate, muçarela, fatias de presunto parma e raspas de parmesão" },
  // 11- ROMANA
  { nome: "ROMANA", ingredientes: "Molho de tomate, muçarela, anchovas, tomate e orégano" },
  // 12- BACON 
  { nome: "BACON", ingredientes: "Molho de tomate, muçarela e fatias crocantes de bacon" },
  // 13- MILHO
  { nome: "MILHO", ingredientes: "Molho de tomate, muçarela e milho verde em conserva" },
  // 14- DOIS QUEIJOS
  { nome: "DOIS QUEIJOS", ingredientes: "Molho de tomate, muçarela e catupiry" },
  // 15- PERA
  { nome: "PERA", ingredientes: "Massa fina, queijo gorgonzola e fatias de pera, regada com mel" },
  // 16- FRANGO COM CHEDDAR
  { nome: "FRANGO COM CHEDDAR", ingredientes: "Molho de tomate, frango desfiado e queijo cheddar cremoso" },
  // 17- PALMITO
  { nome: "PALMITO", ingredientes: "Molho de tomate, muçarela e fatias de palmito" },
  // 18- BRÓCOLIS
  { nome: "BRÓCOLIS", ingredientes: "Molho de tomate, muçarela, brócolis cozido no vapor e alho frito" },
  // 19- CAMPESTRE 
  { nome: "CAMPESTRE", ingredientes: "Molho de tomate, muçarela, palmito, champignon, pimentão e orégano" },
  // 20- NAPOLITANA
  { nome: "NAPOLITANA", ingredientes: "Molho de tomate, muçarela, tomate fatiado, queijo parmesão ralado e orégano" },
  
  // ===================================
  // ## PIZZA DOCE (21 em diante)
  // ===================================
  
  // 21- BRIGADEIRO 
  { nome: "BRIGADEIRO", ingredientes: "Base de chocolate, brigadeiro cremoso e granulado belga" },
  // 22- CHOCOLATE BRANCO
  { nome: "CHOCOLATE BRANCO", ingredientes: "Base de chocolate branco e raspas de chocolate branco" },
  // 23- ROMEU E JULIETA
  { nome: "ROMEU E JULIETA", ingredientes: "Base, muçarela e fatias de goiabada" },
  // 24- BANANA 
  { nome: "BANANA", ingredientes: "Base, banana em rodelas, açúcar, canela e leite condensado" },
  // 25- DO GORDO (Anteriormente: PRESUNTO PICANTE) - **INGREDIENTES ATUALIZADOS**
  { nome: "DO GORDO", ingredientes: "Chocolate, chocolate branco, doce de leite, Nutella, chocolate kinder, alpino, chocotone, confete e molho especial estilo X ratão" },
  // 69- JASON PICANTE - 
  { nome: "JASON PICANTE", ingredientes: "Chocolate gourmet, paçoca, pimenta, tadalafila de 20mg (com link de telegram +18 bônus)" },
];

// O restante do código de desenho e interação (setup, draw, mousePressed, etc.)
// permanece o mesmo que o código anterior para funcionar corretamente.

const MARGEM = 20;
const ALTURA_ITEM = 30;
const COLUNAS = 3; 

let telaAtual = 'menu';
let pizzaSelecionada = null;

function setup() {
  createCanvas(600, 800);
  textAlign(CENTER, CENTER);
  textSize(14);
}

function draw() {
  background(255, 240, 220);

  if (telaAtual === 'menu') {
    desenharMenu();
  } else if (telaAtual === 'ingredientes') {
    desenharIngredientes();
  }
}

function desenharMenu() {
  fill(0);
  textSize(24);
  textStyle(BOLD);
  text("Cardápio de Pizzas 🍕", width / 2, MARGEM * 2);

  // Adicionando os títulos de categoria
  textSize(18);
  textStyle(BOLD);
  text("PIZZA SALGADA", width / 2, MARGEM * 4); // Título para a primeira seção
  
  textStyle(NORMAL);
  textSize(14);

  const larguraColuna = (width - MARGEM * (COLUNAS + 1)) / COLUNAS;

  menuPizzas.forEach((pizza, index) => {
    let num = index + 1;
    let linha, coluna;

    // Lógica para determinar a linha e coluna na grade
    const itensSalgados = 20;
    
    if (num <= itensSalgados) {
        // Pizzas Salgadas (1 a 20)
        const indiceRelativo = index;
        linha = floor(indiceRelativo / COLUNAS);
        coluna = indiceRelativo % COLUNAS;
    } else {
        // Pizzas Doces (21 em diante)
        if (num === 27) return; // Não desenha se for o índice 27/Pizza 27
        
        // Pula uma linha e adiciona o novo título
        if (index === itensSalgados) {
             // Adiciona o título da PIZZA DOCE na posição correta
             textSize(18);
             textStyle(BOLD);
             // A linha do título doce será após a última linha de salgadas
             const linhaTituloDoce = floor((itensSalgados - 1) / COLUNAS) + 2; 
             const yTituloDoce = MARGEM * 5 + linhaTituloDoce * (ALTURA_ITEM + 10) - (ALTURA_ITEM / 2); // Ajuste para ficar acima
             text("PIZZA DOCE", width / 2, yTituloDoce);
             
             // Redefine o estilo para os itens da lista
             textStyle(NORMAL);
             textSize(14);
        }

        const indiceRelativo = index - itensSalgados;
        // Posição ajustada para começar após o título "PIZZA DOCE"
        const offsetLinha = floor((itensSalgados - 1) / COLUNAS) + 3;
        linha = offsetLinha + floor(indiceRelativo / COLUNAS);
        coluna = indiceRelativo % COLUNAS;
    }
    
    // As coordenadas X e Y são calculadas da mesma forma
    const x = MARGEM + coluna * (larguraColuna + MARGEM) + larguraColuna / 2;
    const y = MARGEM * 5 + linha * (ALTURA_ITEM + 10);

    const xRect = x - larguraColuna / 2;
    const yRect = y - ALTURA_ITEM / 2;

    if (mouseX > xRect && mouseX < xRect + larguraColuna &&
      mouseY > yRect && mouseY < yRect + ALTURA_ITEM) {
      fill(255, 200, 100);
      rect(xRect, yRect, larguraColuna, ALTURA_ITEM, 5);
      fill(0);
      textStyle(BOLD);
      cursor(HAND); // Mãozinha ao passar o mouse
    } else {
      fill(220);
      rect(xRect, yRect, larguraColuna, ALTURA_ITEM, 5);
      fill(50);
      textStyle(NORMAL);
      cursor(ARROW); // Seta normal
    }

    // Ajuste para exibir os números 25 (DO GORDO) e 69 (JASON PICANTE)
    let numeroExibido = num;
    if (pizza.nome === "DO GORDO") {
        numeroExibido = 25;
    } else if (pizza.nome === "JASON PICANTE") {
        numeroExibido = 69;
    }
    
    text(`${numeroExibido}- ${pizza.nome}`, x, y);
  });
}

function desenharIngredientes() {
  fill(0);
  textSize(28);
  textStyle(BOLD);
  text(pizzaSelecionada.nome, width / 2, MARGEM * 4);

  textSize(18);
  textStyle(NORMAL);
  fill(50);
  text("Ingredientes:", width / 2, height / 3);

  textSize(16);
  textAlign(LEFT, TOP);
  // Box para os ingredientes
  text(pizzaSelecionada.ingredientes, MARGEM * 3, height / 3 + 30, width - MARGEM * 6, height / 2);
  textAlign(CENTER, CENTER);

  // Botão de voltar
  const botaoX = width / 2;
  const botaoY = height - MARGEM * 3;
  const botaoL = 150;
  const botaoA = 40;

  if (mouseX > botaoX - botaoL / 2 && mouseX < botaoX + botaoL / 2 &&
    mouseY > botaoY - botaoA / 2 && mouseY < botaoY + botaoA / 2) {
    fill(150, 0, 0);
    cursor(HAND);
  } else {
    fill(200, 0, 0);
    cursor(ARROW);
  }
  rect(botaoX - botaoL / 2, botaoY - botaoA / 2, botaoL, botaoA, 8);
  fill(255);
  textSize(16);
  text("<- Voltar ao Menu", botaoX, botaoY);
}

function mousePressed() {
  if (telaAtual === 'menu') {
    handleMenuClick();
  } else if (telaAtual === 'ingredientes') {
    handleIngredientesClick();
  }
}

function handleMenuClick() {
  const larguraColuna = (width - MARGEM * (COLUNAS + 1)) / COLUNAS;
  
  // Adicionar lógica de altura para pular os títulos de categoria ao calcular o clique
  const itensSalgados = 20;

  menuPizzas.forEach((pizza, index) => {
    let num = index + 1;
    let linha, coluna;

    if (num <= itensSalgados) {
        // Pizzas Salgadas (1 a 20)
        const indiceRelativo = index;
        linha = floor(indiceRelativo / COLUNAS);
        coluna = indiceRelativo % COLUNAS;
    } else {
        // Pizzas Doces (21 em diante)
        if (num === 27) return; 

        // Posição ajustada para começar após o título "PIZZA DOCE"
        const offsetLinha = floor((itensSalgados - 1) / COLUNAS) + 3;
        const indiceRelativo = index - itensSalgados;
        linha = offsetLinha + floor(indiceRelativo / COLUNAS);
        coluna = indiceRelativo % COLUNAS;
    }

    const x = MARGEM + coluna * (larguraColuna + MARGEM) + larguraColuna / 2;
    const y = MARGEM * 5 + linha * (ALTURA_ITEM + 10);

    const xRect = x - larguraColuna / 2;
    const yRect = y - ALTURA_ITEM / 2;

    if (mouseX > xRect && mouseX < xRect + larguraColuna &&
      mouseY > yRect && mouseY < yRect + ALTURA_ITEM) {
      pizzaSelecionada = pizza;
      telaAtual = 'ingredientes';
    }
  });
}

function handleIngredientesClick() {
  const botaoX = width / 2;
  const botaoY = height - MARGEM * 3;
  const botaoL = 150;
  const botaoA = 40;

  const xRect = botaoX - botaoL / 2;
  const yRect = botaoY - botaoA / 2;

  if (mouseX > xRect && mouseX < xRect + botaoL &&
    mouseY > yRect && mouseY < yRect + botaoA) {
    telaAtual = 'menu';
    pizzaSelecionada = null;
  }
}