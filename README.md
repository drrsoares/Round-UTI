<!DOCTYPE html>
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
    <!-- Seu HTML existente até onde irá a nova seção de Acesso Central -->
    
    <!-- NOVA SEÇÃO: Acesso Central -->
    <div class="form-group">
      <div class="switch-container">
        <label class="switch">
          <input type="checkbox" id="hasCentralAccess">
          <span class="slider"></span>
        </label>
        <label for="hasCentralAccess">Paciente com Acesso Central</label>
      </div>
    </div>
    
    <div id="centralAccessSection" class="hidden">
      <div class="alert alert-info">
        <i class="fas fa-info-circle"></i> Informações sobre o acesso central do paciente.
      </div>
      
      <div class="flex-container">
        <div>
          <div class="form-group">
            <label for="centralAccessLocation" class="form-label">Localização</label>
            <select id="centralAccessLocation" class="form-control">
              <option value="">Selecione</option>
              <option value="VJD">VJD (Veia Jugular Direita)</option>
              <option value="VJE">VJE (Veia Jugular Esquerda)</option>
              <option value="VSCD">VSCD (Veia Subclávia Direita)</option>
              <option value="VSCE">VSCE (Veia Subclávia Esquerda)</option>
              <option value="VAD">VAD (Veia Axilar Direita)</option>
              <option value="VAE">VAE (Veia Axilar Esquerda)</option>
              <option value="FD">FD (Femoral Direita)</option>
              <option value="FE">FE (Femoral Esquerda)</option>
            </select>
          </div>
        </div>
        <div>
          <div class="form-group">
            <label for="centralAccessInsertionDate" class="form-label">Data de Inserção</label>
            <input type="date" id="centralAccessInsertionDate" class="form-control">
          </div>
        </div>
      </div>
      
      <div class="form-group">
        <label class="form-label">Tempo de Uso</label>
        <div id="centralAccessDuration" class="form-control" style="background-color: var(--input-bg); padding: 0.75rem; border: 1px solid var(--border-color); border-radius: 0.25rem;">
          Informe a data de inserção
        </div>
      </div>
      
      <div class="form-group">
        <label for="centralAccessNotes" class="form-label">Observações</label>
        <textarea id="centralAccessNotes" class="form-control" placeholder="Observações sobre o acesso central"></textarea>
      </div>
    </div>
    
    <!-- Continuar com seu HTML existente -->
  </div>

  <script>
    // Seu JavaScript existente
    
    // Adicione o novo evento na função setupEventListeners
    function setupEventListeners() {
      // Seus eventos existentes
      
      // NOVO: Evento para o checkbox de acesso central
      document.getElementById('hasCentralAccess').addEventListener('change', function() {
        const centralAccessSection = document.getElementById('centralAccessSection');
        centralAccessSection.classList.toggle('hidden', !this.checked);
        
        // Atualizar o cálculo de tempo de uso quando o checkbox for marcado
        if (this.checked) {
          updateCatheterDuration();
        }
      });
      
      // NOVO: Atualizar a duração do cateter quando a data de inserção mudar
      document.getElementById('centralAccessInsertionDate').addEventListener('change', function() {
        updateCatheterDuration();
      });
    }
    
    // NOVA FUNÇÃO: Calcular e atualizar a duração do uso do cateter
    function updateCatheterDuration() {
      const insertionDateInput = document.getElementById('centralAccessInsertionDate');
      const durationElement = document.getElementById('centralAccessDuration');
      
      if (insertionDateInput.value) {
        const insertionDate = new Date(insertionDateInput.value);
        const today = new Date();
        
        // Calcular a diferença em dias
        const differenceInTime = today.getTime() - insertionDate.getTime();
        const differenceInDays = Math.floor(differenceInTime / (1000 * 3600 * 24));
        
        durationElement.textContent = `${differenceInDays} dias`;
        
        // Adicionar alerta visual baseado no tempo de uso
        durationElement.classList.remove('text-success', 'text-warning', 'text-danger');
        
        if (differenceInDays < 7) {
          durationElement.classList.add('text-success');
        } else if (differenceInDays < 14) {
          durationElement.classList.add('text-warning');
        } else {
          durationElement.classList.add('text-danger');
        }
      } else {
        durationElement.textContent = 'Informe a data de inserção';
        durationElement.classList.remove('text-success', 'text-warning', 'text-danger');
      }
    }
    
    // Modificar a função saveRecord para incluir os dados do acesso central
    function saveRecord(event) {
      // Seu código existente
      
      // Adicionar os dados do acesso central ao objeto record
      const centralAccess = document.getElementById('hasCentralAccess').checked ? {
        location: document.getElementById('centralAccessLocation').value,
        insertionDate: document.getElementById('centralAccessInsertionDate').value,
        notes: document.getElementById('centralAccessNotes').value
      } : null;
      
      // Adicionar à estrutura de record existente
      const record = {
        // Suas propriedades de record existentes
        centralAccess: centralAccess
        // Outras propriedades
      };
      
      // Restante da função saveRecord
    }
    
    // Modificar a função viewRecord para exibir informações do acesso central
    function viewRecord(recordId) {
      // Seu código existente
      
      // Verificar se há informações de acesso central
      const hasCentralAccess = record.centralAccess !== null;
      
      // Criar HTML para acesso central
      let centralAccessHtml = '';
      if (hasCentralAccess) {
        const location = record.centralAccess.location;
        const insertionDate = formatDate(record.centralAccess.insertionDate);
        const notes = record.centralAccess.notes || '';
        
        // Calcular o tempo de uso até a data do registro
        const recordDate = new Date(record.date);
        const insertDate = new Date(record.centralAccess.insertionDate);
        const daysOfUse = Math.floor((recordDate - insertDate) / (1000 * 60 * 60 * 24));
        
        centralAccessHtml = `
          <div class="divider"></div>
          <div class="record-central-access">
            <h4>Acesso Central</h4>
            <p><strong>Localização:</strong> ${location}</p>
            <p><strong>Data de Inserção:</strong> ${insertionDate}</p>
            <p><strong>Tempo de Uso:</strong> ${daysOfUse} dias</p>
            ${notes ? `<p><strong>Observações:</strong> ${notes}</p>` : ''}
          </div>
        `;
      }
      
      // Adicionar ao HTML final
      // ${hasCentralAccess ? centralAccessHtml : ''}
    }
  </script>
</body>
</html>
