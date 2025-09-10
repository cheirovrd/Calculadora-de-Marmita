<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistema de Cálculo - Marmitas</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #2c3e50, #1a1a1a);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      color: #333;
    }
    
    .container {
      width: 100%;
      max-width: 800px;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-radius: 20px;
      border: 1px solid rgba(255, 255, 255, 0.18);
      box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
      padding: 30px;
      overflow: hidden;
    }
    
    header {
      text-align: center;
      margin-bottom: 25px;
    }
    
    h2 {
      color: #fff;
      text-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      font-size: 28px;
      margin-bottom: 15px;
    }
    
    .modo-container {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 25px;
      background: rgba(255, 255, 255, 0.1);
      padding: 15px;
      border-radius: 15px;
      backdrop-filter: blur(5px);
      -webkit-backdrop-filter: blur(5px);
      border: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    .modo-switch {
      position: relative;
      display: inline-block;
      width: 80px;
      height: 34px;
    }
    
    .modo-switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }
    
    .slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(255, 255, 255, 0.2);
      transition: .4s;
      border-radius: 34px;
      box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    }
    
    .slider:before {
      position: absolute;
      content: "";
      height: 26px;
      width: 26px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      z-index: 2;
    }
    
    input:checked + .slider:before {
      transform: translateX(46px);
    }
    
    .slider-icon {
      position: absolute;
      color: white;
      font-size: 14px;
      top: 50%;
      transform: translateY(-50%);
      z-index: 1;
    }
    
    .slider-icon.marmita {
      left: 10px;
    }
    
    .slider-icon.ingredientes {
      right: 10px;
    }
    
    .modo-descricao {
      margin-left: 15px;
      font-weight: bold;
      color: #fff;
      text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    }
    
    .form-container {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: 15px;
      padding: 20px;
      margin-bottom: 20px;
      border: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
      color: #fff;
      text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    }
    
    input {
      width: 100%;
      padding: 12px 15px;
      margin-top: 8px;
      border: none;
      border-radius: 10px;
      background: rgba(255, 255, 255, 0.9);
      font-size: 16px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      transition: all 0.3s ease;
      color: #333;
    }
    
    input:focus {
      outline: none;
      box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.5);
      background: rgba(255, 255, 255, 1);
    }
    
    input[readonly] {
      background: rgba(255, 255, 255, 0.7);
      color: #666;
    }
    
    .ingrediente-item {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(5px);
      -webkit-backdrop-filter: blur(5px);
      border-radius: 12px;
      padding: 15px;
      margin-bottom: 15px;
      border: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    .ingrediente-item h4 {
      margin-top: 0;
      color: #fff;
      text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
      margin-bottom: 12px;
      padding-bottom: 8px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
    }
    
    .ingrediente-grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      gap: 12px;
      align-items: end;
    }
    
    .ingrediente-grid div {
      display: flex;
      flex-direction: column;
    }
    
    .ingrediente-grid label {
      font-size: 0.9em;
      margin-bottom: 5px;
    }
    
    button {
      margin-top: 20px;
      padding: 14px;
      width: 100%;
      background: rgba(255, 255, 255, 0.2);
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      backdrop-filter: blur(5px);
      -webkit-backdrop-filter: blur(5px);
      border: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 15px rgba(0, 0, 0, 0.25);
      background: rgba(255, 255, 255, 0.25);
    }
    
    .enter-hint {
      display: block;
      text-align: center;
      margin-top: 10px;
      font-size: 0.9em;
      color: rgba(255, 255, 255, 0.7);
    }
    
    .resultado {
      margin-top: 25px;
      padding: 20px;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: 15px;
      font-weight: bold;
      color: #fff;
      text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
      border: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    .info-text {
      font-size: 0.85em;
      color: rgba(255, 255, 255, 0.7);
      margin-top: 4px;
      font-style: italic;
    }
    
    .calculando {
      opacity: 0.7;
      pointer-events: none;
    }
    
    @media (max-width: 768px) {
      .ingrediente-grid {
        grid-template-columns: 1fr;
        gap: 10px;
      }
      
      .container {
        padding: 20px;
      }
      
      h2 {
        font-size: 24px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h2>📊 Sistema de Cálculo - Marmitas</h2>
    </header>

    <div class="modo-container">
      <label class="modo-switch">
        <input type="checkbox" id="modoToggle" onchange="alternarModo()">
        <span class="slider">
          <i class="slider-icon marmita fas fa-utensils"></i>
          <i class="slider-icon ingredientes fas fa-shopping-cart"></i>
        </span>
      </label>
      <span class="modo-descricao" id="modoAtual">Modo: Marmita</span>
    </div>

    <div class="form-container">
      <form id="formulario">
        <div id="campos"></div>
      </form>

      <label for="quantidade">Número de marmitas produzidas:</label>
      <input type="number" id="quantidade" value="1" min="1" oninput="calcularAutomatico()">
      
      <label for="lucro">Porcentagem de lucro (%):</label>
      <input type="number" id="lucro" value="20" min="0" oninput="calcularAutomatico()">

      <button onclick="calcularPreco()">Calcular Preço</button>
      <span class="enter-hint">Pressione Enter para calcular</span>
    </div>

    <div class="resultado" id="resultado"></div>

    <div class="resultado" id="detalhesIngredientes" style="display: none;">
      <h3>Detalhes dos Ingredientes por Marmita:</h3>
      <div id="listaIngredientes"></div>
    </div>
  </div>

  <script>
    let modo = "marmita"; // marmita ou ingredientes
    let calculoAutomaticoHabilitado = true;

    const camposMarmita = [
      {id:"carne", label:"Preço da carne (R$)", step:"0.01", nomeExibicao: "Carne"},
      {id:"arroz", label:"Preço do arroz (R$)", step:"0.01", nomeExibicao: "Arroz"},
      {id:"batata", label:"Preço das batatas (R$)", step:"0.01", nomeExibicao: "Batata"},
      {id:"tomates", label:"Preço dos tomates (R$)", step:"0.01", nomeExibicao: "Tomates"},
      {id:"queijo", label:"Preço do queijo (R$)", step:"0.01", nomeExibicao: "Queijo"},
      {id:"temperos", label:"Preço dos temperos (R$)", step:"0.01", nomeExibicao: "Temperos"},
      {id:"ovos", label:"Preço dos ovos (R$)", step:"0.01", nomeExibicao: "Ovos"},
      {id:"farinhas", label:"Preço das farinhas (R$)", step:"0.01", nomeExibicao: "Farinhas"},
      {id:"embalagem", label:"Preço da embalagem (R$)", step:"0.01", nomeExibicao: "Embalagem"},
      {id:"gas", label:"Custo do gás (R$)", step:"0.01", nomeExibicao: "Gás"}
    ];

    const camposIngredientes = [
      {id:"carneKg", idQtd:"carneQtd", labelKg:"Preço do kg da carne (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Carne"},
      {id:"arrozKg", idQtd:"arrozQtd", labelKg:"Preço do kg do arroz (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Arroz"},
      {id:"batataKg", idQtd:"batataQtd", labelKg:"Preço do kg da batata (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Batata"},
      {id:"tomateKg", idQtd:"tomateQtd", labelKg:"Preço do kg do tomate (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Tomate"},
      {id:"queijoKg", idQtd:"queijoQtd", labelKg:"Preço do kg do queijo (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Queijo"},
      {id:"temperoKg", idQtd:"temperoQtd", labelKg:"Preço do kg dos temperos (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Temperos"},
      {id:"ovoDz", idQtd:"ovoQtd", labelKg:"Preço da dúzia de ovos (R$)", labelQtd:"Quant. usada (unid.)", step:"0.01", nomeExibicao: "Ovos", tipo: "duzia"},
      {id:"farinhaKg", idQtd:"farinhaQtd", labelKg:"Preço do kg da farinha (R$)", labelQtd:"Quant. usada (g)", step:"0.01", nomeExibicao: "Farinha"},
      {id:"embalagem", label:"Preço da embalagem (R$)", step:"0.01", nomeExibicao: "Embalagem", isCustoDireto: true},
      {id:"gas", label:"Custo do gás (R$)", step:"0.01", nomeExibicao: "Gás", isCustoDireto: true}
    ];

    function getInputValue(id) {
        const value = parseFloat(document.getElementById(id).value);
        return isNaN(value) ? 0 : value;
    }

    function renderCampos() {
      let campos = (modo === "marmita") ? camposMarmita : camposIngredientes;
      let html = "";
      campos.forEach(c => {
        if (modo === "marmita") {
            html += `
              <label for="${c.id}">${c.label}</label>
              <input type="number" id="${c.id}" step="${c.step}" oninput="calcularAutomatico()">
              <div class="info-text">Custo total com ${c.nomeExibicao.toLowerCase()}</div>
            `;
        } else {
            if (c.isCustoDireto) {
                html += `
                    <label for="${c.id}">${c.label}</label>
                    <input type="number" id="${c.id}" step="${c.step}" oninput="calcularAutomatico()">
                    <div class="info-text">Custo fixo com ${c.nomeExibicao.toLowerCase()}</div>
                `;
            } else {
                html += `
                    <div class="ingrediente-item">
                        <h4>${c.nomeExibicao}</h4>
                        <div class="ingrediente-grid">
                            <div>
                                <label for="${c.id}">${c.labelKg}</label>
                                <input type="number" id="${c.id}" step="${c.step}" oninput="calcularCustoIngrediente('${c.id}', '${c.idQtd}', '${c.tipo || 'gramas'}')">
                            </div>
                            <div>
                                <label for="${c.idQtd}">${c.labelQtd}</label>
                                <input type="number" id="${c.idQtd}" step="1" oninput="calcularCustoIngrediente('${c.id}', '${c.idQtd}', '${c.tipo || 'gramas'}')">
                            </div>
                            <div>
                                <label>Custo na marmita (R$)</label>
                                <input type="text" id="custo${c.id}" readonly>
                            </div>
                        </div>
                    </div>
                `;
            }
        }
      });
      document.getElementById("campos").innerHTML = html;
      document.getElementById("modoAtual").innerText =
        "Modo: " + (modo === "marmita" ? "Marmita" : "Ingredientes");

      document.getElementById("detalhesIngredientes").style.display = "none";
      document.getElementById("modoToggle").checked = modo === "ingredientes";
      
      // Adicionar event listener para a tecla Enter em todos os campos de entrada
      const inputs = document.querySelectorAll('input');
      inputs.forEach(input => {
        input.addEventListener('keypress', function(e) {
          if (e.key === 'Enter') {
            e.preventDefault();
            calcularPreco();
          }
        });
      });
    }

    function alternarModo() {
      modo = (modo === "marmita") ? "ingredientes" : "marmita";
      renderCampos();
      calcularAutomatico();
    }

    function calcularCustoIngrediente(idPreco, idQuantidade, tipo) {
      if (modo !== "ingredientes") return;
      
      const preco = getInputValue(idPreco);
      const quantidade = getInputValue(idQuantidade);
      let custo = 0;
      
      if (tipo === 'duzia') {
        custo = (preco / 12) * quantidade;
      } else {
        custo = (preco / 1000) * quantidade;
      }
      
      document.getElementById(`custo${idPreco}`).value = custo.toFixed(2);
      calcularAutomatico();
    }

    function calcularAutomatico() {
      if (!calculoAutomaticoHabilitado) return;
      
      // Pequeno atraso para evitar cálculos desnecessários durante digitação
      clearTimeout(window.calculoTimeout);
      window.calculoTimeout = setTimeout(() => {
        document.getElementById('resultado').innerHTML = "<div class='calculando'>Calculando...</div>";
        
        let custoTotal = 0;
        
        if (modo === "marmita") {
          camposMarmita.forEach(c => {
            custoTotal += getInputValue(c.id);
          });
        } else {
          camposIngredientes.forEach(c => {
            if (c.isCustoDireto) {
              custoTotal += getInputValue(c.id);
            } else if (c.tipo === "duzia") {
              const precoDuzia = getInputValue(c.id);
              const qtdOvos = getInputValue(c.idQtd);
              custoTotal += (precoDuzia / 12) * qtdOvos;
            } else {
              const precoKg = getInputValue(c.id);
              const qtdGramas = getInputValue(c.idQtd);
              custoTotal += (precoKg / 1000) * qtdGramas;
            }
          });
        }
        
        const quantidade = getInputValue("quantidade");
        const custoUnitario = quantidade > 0 ? custoTotal / quantidade : 0;
        
        document.getElementById('resultado').innerHTML = `
          💵 Custo por Marmita: <strong>R$ ${custoUnitario.toFixed(2)}</strong>
          <div class="info-text">Valor atualizado automaticamente</div>
        `;
      }, 500);
    }

    function calcularPreco() {
      calculoAutomaticoHabilitado = false;
      
      setTimeout(() => {
        let custoTotal = 0;
        let custosIndividuais = {};

        if (modo === "marmita") {
          camposMarmita.forEach(c => {
            let valor = getInputValue(c.id);
            custoTotal += valor;
            custosIndividuais[c.nomeExibicao] = valor;
          });
        } else {
          camposIngredientes.forEach(c => {
            let custoItem = 0;
            if (c.isCustoDireto) {
              custoItem = getInputValue(c.id);
            } else if (c.tipo === "duzia") {
              let precoDuzia = getInputValue(c.id);
              let qtdOvos = getInputValue(c.idQtd);
              custoItem = (precoDuzia / 12) * qtdOvos;
            } else {
              let precoKg = getInputValue(c.id);
              let qtdGramas = getInputValue(c.idQtd);
              custoItem = (precoKg / 1000) * qtdGramas;
            }
            custoTotal += custoItem;
            custosIndividuais[c.nomeExibicao] = custoItem;
          });
        }

        let quantidade = getInputValue("quantidade");
        let custoUnitario = quantidade > 0 ? custoTotal / quantidade : 0;

        let lucroPercent = getInputValue("lucro");
        let precoVendaUnitario = custoUnitario * (1 + lucroPercent / 100);

        document.getElementById("resultado").innerHTML = `
          📌 Custo Total da Produção: <strong>R$ ${custoTotal.toFixed(2)}</strong><br>
          🍽️ Número de Marmitas: <strong>${quantidade}</strong><br>
          💵 Custo por Marmita: <strong>R$ ${custoUnitario.toFixed(2)}</strong><br>
          📈 Preço de Venda (com ${lucroPercent}% de lucro): <strong>R$ ${precoVendaUnitario.toFixed(2)}</strong>
        `;

        if (modo === "ingredientes") {
          let listaHtml = "";
          for (const nomeIngrediente in custosIndividuais) {
            let custoPorMarmita = quantidade > 0 ? custosIndividuais[nomeIngrediente] / quantidade : 0;
            listaHtml += `
              <p><strong>${nomeIngrediente}:</strong> R$ ${custoPorMarmita.toFixed(2)}</p>
            `;
          }
          document.getElementById("listaIngredientes").innerHTML = listaHtml;
          document.getElementById("detalhesIngredientes").style.display = "block";
        } else {
          document.getElementById("detalhesIngredientes").style.display = "none";
        }
        
        calculoAutomaticoHabilitado = true;
      }, 100);
    }

    // Inicializa os campos
    renderCampos();
    
    // Adicionar event listener global para a tecla Enter
    document.addEventListener('keypress', function(e) {
      if (e.key === 'Enter') {
        e.preventDefault();
        calcularPreco();
      }
    });
  </script>
</body>
</html>
