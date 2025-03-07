<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistema de Acompanhamento de Pacientes</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    /* Seu CSS existente */
  </style>
</head>
<body>
  <div class="container">
    <!-- Conteúdo existente... -->
    
    <!-- Modificação na seção de intubação para incluir data de início e cálculo do tempo -->
    <div id="intubationSection" class="hidden">
      <div class="alert alert-info">
        <i class="fas fa-info-circle"></i> Informações adicionais para paciente intubado.
      </div>
      
      <div class="flex-container">
        <div>
          <div class="form-group">
            <label for="intubationStartDate" class="form-label">Data de Início da Intubação</label>
            <input type="date" id="intubationStartDate" class="form-control">
          </div>
        </div>
        <div>
          <div class="form-group">
            <label class="form-label">Tempo de Intubação</label>
            <div id="intubationDuration" class="form-control" style="background-color: var(--input-bg); padding: 0.75rem; border: 1px solid var(--border-color); border-radius: 0.25rem;">
              Informe a data de início
            </div>
          </div>
        </div>
      </div>
      
      <div class="form-group">
        <label for="canBeExtubated" class="form-label required-field">O paciente pode ser extubado?</label>
        <div class="radio-group">
          <label class="radio-container" style="margin-right: 20px; display: inline-block;">
            <input type="radio" name="canBeExtubated" value="S"> Sim
          </label>
          <label class="radio-container" style="display: inline-block;">
            <input type="radio" name="canBeExtubated" value="N"> Não
          </label>
        </div>
      </div>
      
      <div class="card" style="padding: 1rem; margin-bottom: 1rem; background-color: rgba(93, 92, 222, 0.05);">
        <h4>Parâmetros de Ventilação Mecânica</h4>
        
        <!-- Outros campos de ventilação mecânica existentes -->
      </div>
      
      <div class="form-group">
        <label for="intubationNotes" class="form-label">Observações sobre intubação</label>
        <textarea id="intubationNotes" class="form-control notes-field" placeholder="Informe detalhes relevantes sobre a intubação ou condições respiratórias"></textarea>
      </div>
    </div>
    
    <!-- Resto do conteúdo existente... -->
  </div>

  <script>
    // JavaScript existente...
    
    // Adicionar eventos para o cálculo do tempo de intubação
    function setupEventListeners() {
      // Eventos existentes...
      
      // Evento de checkbox de intubação
      document.getElementById('isIntubated').addEventListener('change', function() {
        const intubationSection = document.getElementById('intubationSection');
        intubationSection.classList.toggle('hidden', !this.checked);
        
        // Se o checkbox for marcado, atualizar o cálculo de tempo de intubação
        if (this.checked) {
          updateIntubationDuration();
        }
      });
      
      // Atualizar a duração da intubação quando a data de início mudar
      document.getElementById('intubationStartDate').addEventListener('change', function() {
        updateIntubationDuration();
      });
      
      // Outros eventos existentes...
    }
    
    // Função para calcular e atualizar o tempo de intubação
    function updateIntubationDuration() {
      const startDateInput = document.getElementById('intubationStartDate');
      const durationElement = document.getElementById('intubationDuration');
      
      if (startDateInput.value) {
        const startDate = new Date(startDateInput.value);
        const today = new Date();
        
        // Calcular a diferença em dias
        const differenceInTime = today.getTime() - startDate.getTime();
        const differenceInDays = Math.floor(differenceInTime / (1000 * 3600 * 24));
        
        durationElement.textContent = `${differenceInDays} dias`;
        
        // Adicionar alerta visual baseado no tempo de intubação
        durationElement.classList.remove('text-success', 'text-warning', 'text-danger');
        
        if (differenceInDays < 7) {
          durationElement.classList.add('text-success');
        } else if (differenceInDays < 14) {
          durationElement.classList.add('text-warning');
        } else {
          durationElement.classList.add('text-danger');
        }
      } else {
        durationElement.textContent = 'Informe a data de início';
        durationElement.classList.remove('text-success', 'text-warning', 'text-danger');
      }
    }
    
    // Modificar a função saveRecord para incluir a data de início e o tempo de intubação
    function saveRecord(event) {
      // Código existente...
      
      // Atualizar a estrutura de dados da intubação
      const record = {
        // Outras propriedades existentes...
        intubation: document.getElementById('isIntubated').checked ? {
          startDate: document.getElementById('intubationStartDate').value,
          canBeExtubated: document.querySelector('input[name="canBeExtubated"]:checked')?.value || null,
          notes: document.getElementById('intubationNotes').value || '',
          ventilationParams: {
            // Parâmetros de ventilação existentes...
          }
        } : null,
        // Outras propriedades...
      };
      
      // Resto da função saveRecord...
    }
    
    // Modificar a função viewRecord para exibir informações sobre o tempo de intubação
    function viewRecord(recordId) {
      // Código existente...
      
      // Verificar se há informações de intubação
      const hasIntubation = record.intubation !== null;
      
      // Atualizar o HTML para incluir informações sobre o tempo de intubação
      if (hasIntubation && record.intubation.startDate) {
        const startDate = formatDate(record.intubation.startDate);
        
        // Calcular o tempo de intubação até a data do registro
        const recordDate = new Date(record.date);
        const intubStartDate = new Date(record.intubation.startDate);
        const daysIntubated = Math.floor((recordDate - intubStartDate) / (1000 * 60 * 60 * 24));
        
        // Adicionar ao HTML da seção de intubação
        // Exemplo:
        /*
        let intubationHtml = `
          <div class="record-intubation">
            <h4>Informações de Intubação</h4>
            <p><strong>Data de Início:</strong> ${startDate}</p>
            <p><strong>Tempo de Intubação:</strong> ${daysIntubated} dias</p>
            <p><strong>Pode ser extubado?</strong> ${record.intubation.canBeExtubated === 'S' ? 'Sim' : record.intubation.canBeExtubated === 'N' ? 'Não' : 'Não informado'}</p>
            ${ventilationHtml}
            ${record.intubation.notes ? `<p><strong>Observações sobre intubação:</strong> ${record.intubation.notes}</p>` : ''}
          </div>
        `;
        */
      }
      
      // Resto da função viewRecord...
    }
    
    // Resto do JavaScript existente...
  </script>
</body>
</html>
