<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analisador de Bilhete do Bicho</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 30px;
        }
        
        header {
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #4CAF50 0%, #2E7D32 100%);
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        
        header h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .app-container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
        }
        
        .input-section, .quotation-section {
            flex: 1;
            min-width: 300px;
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .section-title {
            font-size: 1.4rem;
            margin-bottom: 20px;
            color: #2E7D32;
            border-bottom: 2px solid #E8F5E9;
            padding-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: #4CAF50;
        }
        
        textarea {
            width: 100%;
            height: 200px;
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            resize: vertical;
            transition: border-color 0.3s;
        }
        
        textarea:focus {
            outline: none;
            border-color: #4CAF50;
        }
        
        .quotation-display {
            background-color: #F1F8E9;
            padding: 20px;
            border-radius: 8px;
            margin-top: 15px;
        }
        
        .quotation-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #E8F5E9;
        }
        
        .quotation-item:last-child {
            border-bottom: none;
        }
        
        .quotation-label {
            font-weight: bold;
            color: #1B5E20;
        }
        
        .quotation-value {
            font-weight: bold;
            color: #2E7D32;
            font-size: 1.1rem;
            cursor: pointer;
        }
        
        .quotation-value:hover {
            color: #1B5E20;
            text-decoration: underline;
        }
        
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 25px;
        }
        
        button {
            padding: 14px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            flex: 1;
            min-width: 200px;
        }
        
        .analyze-btn {
            background-color: #2196F3;
            color: white;
        }
        
        .analyze-btn:hover {
            background-color: #0b7dda;
            transform: translateY(-2px);
        }
        
        .whatsapp-btn {
            background-color: #25D366;
            color: white;
        }
        
        .whatsapp-btn:hover {
            background-color: #1da851;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(37, 211, 102, 0.3);
        }
        
        .whatsapp-print-btn {
            background-color: #128C7E;
            color: white;
        }
        
        .whatsapp-print-btn:hover {
            background-color: #0d6d63;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(18, 140, 126, 0.3);
        }
        
        .reset-btn {
            background-color: #f5f5f5;
            color: #666;
            border: 1px solid #ddd;
        }
        
        .reset-btn:hover {
            background-color: #e0e0e0;
        }
        
        .ticket-preview {
            margin-top: 30px;
            background-color: #fff;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .ticket-preview h3 {
            color: #2E7D32;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        #printableTicket {
            background-color: #ffffff;
            padding: 30px;
            border-radius: 10px;
            border: 2px solid #4CAF50;
            max-width: 500px;
            margin: 0 auto;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            font-family: 'Courier New', monospace;
            position: relative;
        }
        
        .ticket-content {
            white-space: pre-line;
            line-height: 1.6;
            font-size: 1.1rem;
            color: #333;
        }
        
        .ticket-divider {
            height: 2px;
            background: linear-gradient(to right, transparent, #4CAF50, transparent);
            margin: 20px 0;
        }
        
        .ticket-quotation {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px dashed #4CAF50;
        }
        
        .ticket-quotation-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            font-size: 1.1rem;
        }
        
        .instructions {
            background-color: #FFF8E1;
            border-left: 5px solid #FFC107;
            padding: 20px;
            border-radius: 8px;
            margin-top: 30px;
        }
        
        .instructions h3 {
            color: #FF9800;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .instructions ul {
            padding-left: 20px;
        }
        
        .instructions li {
            margin-bottom: 10px;
        }
        
        footer {
            text-align: center;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #ddd;
            color: #666;
            font-size: 0.9rem;
        }
        
        .sample-ticket {
            margin-top: 15px;
            font-size: 0.9rem;
            color: #666;
            font-style: italic;
        }
        
        .whatsapp-notice {
            background-color: #dcf8c6;
            padding: 12px;
            border-radius: 8px;
            margin-top: 15px;
            border-left: 4px solid #25D366;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .whatsapp-notice i {
            color: #25D366;
            font-size: 1.2rem;
        }
        
        .button-group {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            width: 100%;
        }
        
        @media (max-width: 768px) {
            .app-container {
                flex-direction: column;
            }
            
            button {
                min-width: 100%;
            }
            
            header h1 {
                font-size: 1.8rem;
            }
            
            #printableTicket {
                padding: 20px;
            }
        }
        
        .loading {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            color: white;
            font-size: 1.5rem;
        }
        
        .loading.active {
            display: flex;
        }
        
        .spinner {
            border: 8px solid #f3f3f3;
            border-top: 8px solid #25D366;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 1s linear infinite;
            margin-bottom: 20px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="loading" id="loading">
        <div class="spinner"></div>
        <p>Gerando print do bilhete...</p>
    </div>
    
    <div class="container">
        <header>
            <h1><i class="fas fa-paw"></i> Analisador de Bilhete</h1>
            <p>Cole seu bilhete, visualize as cotações e envie para o WhatsApp</p>
        </header>
        
        <div class="app-container">
            <div class="input-section">
                <h2 class="section-title"><i class="fas fa-ticket-alt"></i> Bilhete</h2>
                <textarea id="ticketInput" placeholder="Cole o bilhete aqui..."></textarea>
                <div class="sample-ticket">
                    <p><strong>Exemplo:</strong> "Número: 5678 - Animal: Vaca - Valor: R$ 5,00"</p>
                </div>
                
                <div class="controls">
                    <button class="analyze-btn" id="analyzeBtn">
                        <i class="fas fa-chart-line"></i> Atualizar Prévia
                    </button>
                    <button class="reset-btn" id="resetBtn">
                        <i class="fas fa-redo"></i> Limpar
                    </button>
                </div>
            </div>
            
            <div class="quotation-section">
                <h2 class="section-title"><i class="fas fa-list-alt"></i> Cotação</h2>
                <div class="quotation-display" id="quotationDisplay">
                    <div class="quotation-item">
                        <span class="quotation-label">Milhar:</span>
                        <span class="quotation-value" id="milharValue" title="Clique para editar">8000</span>
                    </div>
                    <div class="quotation-item">
                        <span class="quotation-label">Centena:</span>
                        <span class="quotation-value" id="centenaValue" title="Clique para editar">800</span>
                    </div>
                    <div class="quotation-item">
                        <span class="quotation-label">Grupo:</span>
                        <span class="quotation-value" id="grupoValue" title="Clique para editar">21</span>
                    </div>
                    <div class="quotation-item">
                        <span class="quotation-label">Terno de Dezena:</span>
                        <span class="quotation-value" id="ternoValue" title="Clique para editar">10.000</span>
                    </div>
                </div>
                
                <div class="whatsapp-notice">
                    <i class="fab fa-whatsapp"></i>
                    <span>Escolha como deseja enviar para o WhatsApp</span>
                </div>
                
                <div class="controls">
                    <div class="button-group">
                        <button class="whatsapp-btn" id="whatsappBtn">
                            <i class="fab fa-whatsapp"></i> Enviar Texto
                        </button>
                        <button class="whatsapp-print-btn" id="whatsappPrintBtn">
                            <i class="fas fa-camera"></i> Enviar Print
                        </button>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="ticket-preview">
            <h3><i class="fas fa-eye"></i> Prévia do Bilhete</h3>
            <div id="printableTicket">
                <div class="ticket-content" id="ticketContent">
                    Seu bilhete será mostrado aqui...
                </div>
                <div class="ticket-divider"></div>
                <div class="ticket-quotation">
                    <div class="ticket-quotation-item">
                        <span>Milhar:</span>
                        <span id="previewMilhar">8000</span>
                    </div>
                    <div class="ticket-quotation-item">
                        <span>Centena:</span>
                        <span id="previewCentena">800</span>
                    </div>
                    <div class="ticket-quotation-item">
                        <span>Grupo:</span>
                        <span id="previewGrupo">21</span>
                    </div>
                    <div class="ticket-quotation-item">
                        <span>Terno de Dezena:</span>
                        <span id="previewTerno">10.000</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="instructions">
            <h3><i class="fas fa-info-circle"></i> Como usar</h3>
            <ul>
                <li>Cole o texto do seu bilhete na área de texto à esquerda</li>
                <li>Clique em "Atualizar Prévia" para processar as informações</li>
                <li>As cotações serão exibidas à direita (clique sobre os valores para editar)</li>
                <li><strong>Enviar Texto:</strong> Envia apenas o texto para o WhatsApp</li>
                <li><strong>Enviar Print:</strong> Captura a tela do bilhete e envia como imagem</li>
                <li>Use o botão "Limpar" para começar novamente</li>
            </ul>
        </div>
        
        <footer>
            <p>Aplicação desenvolvida para facilitar a visualização de cotações</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Elementos DOM
            const ticketInput = document.getElementById('ticketInput');
            const analyzeBtn = document.getElementById('analyzeBtn');
            const resetBtn = document.getElementById('resetBtn');
            const whatsappBtn = document.getElementById('whatsappBtn');
            const whatsappPrintBtn = document.getElementById('whatsappPrintBtn');
            const loading = document.getElementById('loading');
            
            // Elementos de cotação
            const milharValue = document.getElementById('milharValue');
            const centenaValue = document.getElementById('centenaValue');
            const grupoValue = document.getElementById('grupoValue');
            const ternoValue = document.getElementById('ternoValue');
            
            // Elementos de prévia
            const ticketContent = document.getElementById('ticketContent');
            const previewMilhar = document.getElementById('previewMilhar');
            const previewCentena = document.getElementById('previewCentena');
            const previewGrupo = document.getElementById('previewGrupo');
            const previewTerno = document.getElementById('previewTerno');
            
            // Exemplo de bilhete para facilitar testes
            const sampleTicket = `Número: 3456
Animal: Jacaré
Valor: R$ 10,00
Data: ${new Date().toLocaleDateString('pt-BR')}
Local: Ponto de Venda 123`;

            // Inserir bilhete de exemplo no textarea
            ticketInput.value = sampleTicket;
            
            // Atualizar prévia do bilhete
            updateTicketPreview();
            
            // Função para atualizar a prévia
            analyzeBtn.addEventListener('click', function() {
                const ticketText = ticketInput.value.trim();
                
                if (!ticketText) {
                    alert('Por favor, cole um bilhete para análise.');
                    return;
                }
                
                // Atualizar a prévia
                updateTicketPreview();
                
                // Mostrar confirmação
                alert('Bilhete atualizado com sucesso!');
            });
            
            // Função para atualizar a prévia do bilhete
            function updateTicketPreview() {
                const ticketText = ticketInput.value.trim() || 'Bilhete não informado...';
                
                // Atualizar conteúdo do bilhete
                ticketContent.textContent = ticketText;
                
                // Atualizar valores na prévia
                previewMilhar.textContent = milharValue.textContent;
                previewCentena.textContent = centenaValue.textContent;
                previewGrupo.textContent = grupoValue.textContent;
                previewTerno.textContent = ternoValue.textContent;
            }
            
            // Permitir edição direta das cotações
            const quotationValues = [milharValue, centenaValue, grupoValue, ternoValue];
            const previewValues = [previewMilhar, previewCentena, previewGrupo, previewTerno];
            
            quotationValues.forEach((element, index) => {
                element.addEventListener('click', function() {
                    const currentValue = this.textContent;
                    const label = this.parentElement.querySelector('.quotation-label').textContent.replace(':', '');
                    const newValue = prompt(`Editar valor de "${label}":`, currentValue);
                    
                    if (newValue !== null && newValue.trim() !== '') {
                        this.textContent = newValue.trim();
                        previewValues[index].textContent = newValue.trim();
                    }
                });
            });
            
            // Função para enviar TEXTO para o WhatsApp
            whatsappBtn.addEventListener('click', function() {
                const ticketText = ticketInput.value.trim();
                
                if (!ticketText || ticketText === 'Bilhete não informado...') {
                    alert('Por favor, insira um bilhete antes de enviar.');
                    return;
                }
                
                // Formatar a mensagem simples
                const message = `${ticketText}

COTAÇÃO:
Milhar: ${milharValue.textContent}
Centena: ${centenaValue.textContent}
Grupo: ${grupoValue.textContent}
Terno de Dezena: ${ternoValue.textContent}`;
                
                // Formatar a mensagem para URL do WhatsApp
                const encodedMessage = encodeURIComponent(message);
                const whatsappURL = `https://wa.me/?text=${encodedMessage}`;
                
                // Abrir o WhatsApp em uma nova janela
                window.open(whatsappURL, '_blank');
            });
            
            // Função para enviar PRINT para o WhatsApp
            whatsappPrintBtn.addEventListener('click', function() {
                const ticketText = ticketInput.value.trim();
                
                if (!ticketText || ticketText === 'Bilhete não informado...') {
                    alert('Por favor, insira um bilhete antes de enviar.');
                    return;
                }
                
                // Mostrar loading
                loading.classList.add('active');
                
                // Capturar a tela do bilhete
                html2canvas(document.getElementById('printableTicket'), {
                    backgroundColor: '#ffffff',
                    scale: 2, // Aumenta a qualidade da imagem
                    useCORS: true
                }).then(canvas => {
                    // Converter canvas para imagem
                    const image = canvas.toDataURL('image/png');
                    
                    // Criar um link temporário para download
                    const link = document.createElement('a');
                    link.href = image;
                    link.download = 'bilhete_bicho.png';
                    
                    // Criar um blob a partir da imagem
                    canvas.toBlob(function(blob) {
                        // Criar um arquivo a partir do blob
                        const file = new File([blob], "bilhete_bicho.png", { type: "image/png" });
                        
                        // Criar um FormData e adicionar o arquivo
                        const formData = new FormData();
                        formData.append('file', file);
                        
                        // Esconder loading
                        loading.classList.remove('active');
                        
                        // Para enviar pelo WhatsApp Web, precisamos de uma abordagem diferente
                        // Vamos criar um link de compartilhamento com a imagem
                        const whatsappURL = `https://wa.me/?text=${encodeURIComponent('Confira meu bilhete do jogo:')}`;
                        
                        // Abrir WhatsApp
                        window.open(whatsappURL, '_blank');
                        
                        // Mensagem informativa
                        setTimeout(() => {
                            alert('O WhatsApp foi aberto. Para enviar o print:\n\n1. Clique no ícone de anexo (clip)\n2. Escolha "Galeria" ou "Documentos"\n3. Selecione a imagem "bilhete_bicho.png" que foi baixada');
                        }, 1000);
                        
                        // Forçar download da imagem
                        link.click();
                        
                    }, 'image/png');
                }).catch(error => {
                    console.error('Erro ao capturar tela:', error);
                    loading.classList.remove('active');
                    alert('Erro ao gerar o print. Tente novamente.');
                });
            });
            
            // Função para resetar o aplicativo
            resetBtn.addEventListener('click', function() {
                if (confirm('Tem certeza que deseja limpar todo o bilhete?')) {
                    ticketInput.value = '';
                    
                    // Resetar valores padrão das cotações
                    milharValue.textContent = '8000';
                    centenaValue.textContent = '800';
                    grupoValue.textContent = '21';
                    ternoValue.textContent = '10.000';
                    
                    // Atualizar prévias
                    updateTicketPreview();
                }
            });
            
            // Atualizar prévia quando o bilhete for alterado
            ticketInput.addEventListener('input', function() {
                updateTicketPreview();
            });
        });
    </script>
</body>
</html>
