<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>Round Matinal - UTI</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/flowbite@1.6.5/dist/flowbite.min.css" rel="stylesheet">
    <style>
      :root {
        --primary-color: #5D5CDE;
        --warning-color: #FFC107;
        --danger-color: #DC3545;
        --success-color: #28A745;
      }

      /* Dark mode variables */
      @media (prefers-color-scheme: dark) {
        :root {
          --bg-color: #181818;
          --text-color: #f0f0f0;
          --card-bg: #2a2a2a;
          --border-color: #444;
        }
      }

      /* Light mode variables */
      @media (prefers-color-scheme: light) {
        :root {
          --bg-color: #FFFFFF;
          --text-color: #333333;
          --card-bg: #FFFFFF;
          --border-color: #e0e0e0;
        }
      }

      body {
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
        background-color: var(--bg-color);
        color: var(--text-color);
        margin: 0;
        padding: 0;
        transition: background-color 0.3s, color 0.3s;
        -webkit-tap-highlight-color: transparent;
      }

      .container {
        max-width: 1000px;
        margin: 0 auto;
        padding: 1rem;
      }

      .card {
        background-color: var(--card-bg);
        border-radius: 0.5rem;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        padding: 1.5rem;
        margin-bottom: 1.5rem;
        border: 1px solid var(--border-color);
        transition: box-shadow 0.3s ease;
      }

      .card:hover {
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
      }

      h1, h2, h3 {
        color: var(--primary-color);
        margin-bottom: 1rem;
      }

      .btn {
        padding: 0.5rem 1rem;
        border-radius: 0.25rem;
        font-weight: 500;
        cursor: pointer;
        transition: all 0.2s ease;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border: none;
        min-height: 2.5rem;
      }

      .btn-primary {
        background-color: var(--primary-color);
        color: white;
      }

      .btn-primary:hover {
        background-color: #4a49b9;
      }

      .btn-danger {
        background-color: var(--danger-color);
        color: white;
      }

      .btn-danger:hover {
        background-color: #c82333;
      }
      
      .btn-success {
        background-color: var(--success-color);
        color: white;
      }
      
      .btn-success:hover {
        background-color: #218838;
      }
      
      .btn-warning {
        background-color: var(--warning-color);
        color: #212529;
      }
      
      .btn-warning:hover {
        background-color: #e0a800;
      }

      .btn-group {
        display: flex;
        gap: 0.5rem;
        margin-top: 1rem;
        flex-wrap: wrap;
      }

      @media (max-width: 768px) {
        .btn-group {
          flex-direction: column;
        }
        
        .btn {
          width: 100%;
        }
      }

      .form-group {
        margin-bottom: 1rem;
      }

      .form-control {
        width: 100%;
        padding: 0.75rem;
        border: 1px solid var(--border-color);
        border-radius: 0.25rem;
        font-size: 1rem;
        transition: border-color 0.2s ease-in-out;
        background-color: var(--bg-color);
        color: var(--text-color);
      }

      .form-control:focus {
        border-color: var(--primary-color);
        outline: none;
        box-shadow: 0 0 0 2px rgba(93, 92, 222, 0.25);
      }

      .form-label {
        display: block;
        margin-bottom: 0.5rem;
        font-weight: 500;
      }

      .invalid {
        border-color: var(--danger-color) !important;
      }

      .validation-message {
        color: var(--danger-color);
        font-size: 0.875rem;
        margin-top: 0.25rem;
      }

      .alert {
        padding: 1rem;
        border-radius: 0.25rem;
        margin-bottom: 1rem;
      }

      .alert-warning {
        background-color: rgba(255, 193, 7, 0.2);
        border: 1px solid var(--warning-color);
        color: #856404;
      }

      .alert-danger {
        background-color: rgba(220, 53, 69, 0.2);
        border: 1px solid var(--danger-color);
        color: #721c24;
      }
      
      .alert-success {
        background-color: rgba(40, 167, 69, 0.2);
        border: 1px solid var(--success-color);
        color: #155724;
      }

      .hidden {
        display: none !important;
      }

      .flex-container {
        display: flex;
        gap: 1rem;
        margin-bottom: 1rem;
      }

      .flex-container > div {
        flex: 1;
      }

      .medication-entry {
        border: 1px solid var(--border-color);
        border-radius: 0.25rem;
        padding: 1rem;
        margin-bottom: 1rem;
        background-color: rgba(0, 0, 0, 0.02);
      }

      .status-indicator {
        display: inline-block;
        width: 12px;
        height: 12px;
        border-radius: 50%;
        margin-left: 0.5rem;
      }

      .status-ok {
        background-color: var(--success-color);
      }

      .status-warning {
        background-color: var(--warning-color);
      }

      .status-danger {
        background-color: var(--danger-color);
      }

      .status-container {
        display: flex;
        align-items: center;
      }

      /* Tabs */
      .tabs {
        display: flex;
        flex-wrap: wrap;
        border-bottom: 1px solid var(--border-color);
        margin-bottom: 1.5rem;
      }

      .tab {
        padding: 0.75rem 1.25rem;
        cursor: pointer;
        transition: all 0.2s ease;
        border-bottom: 2px solid transparent;
        font-weight: 500;
      }

      .tab.active {
        color: var(--primary-color);
        border-bottom: 2px solid var(--primary-color);
      }

      .tab-content {
        display: none;
      }

      .tab-content.active {
        display: block;
      }

      .checkbox-container {
        display: flex;
        align-items: center;
        margin-bottom: 1rem;
      }

      .checkbox-container input[type="checkbox"] {
        width: auto;
        margin-right: 0.5rem;
      }

      .checkbox-container label {
        display: inline;
        font-weight: normal;
      }

      /* Loading Spinner */
      .spinner {
        width: 40px;
        height: 40px;
        border: 4px solid rgba(93, 92, 222, 0.1);
        border-left-color: var(--primary-color);
        border-radius: 50%;
        animation: spin 1s linear infinite;
        margin: 2rem auto;
      }

      @keyframes spin {
        to { transform: rotate(360deg); }
      }

      /* Toast Notification */
      .toast {
        position: fixed;
        top: 1rem;
        right: 1rem;
        padding: 1rem;
        background-color: var(--primary-color);
        color: white;
        border-radius: 0.25rem;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        opacity: 0;
        transition: opacity 0.3s ease;
        z-index: 1000;
        max-width: 90%;
      }

      .toast.show {
        opacity: 1;
      }

      @media (max-width: 768px) {
        .flex-container {
          flex-direction: column;
        }
        
        .flex-container > div {
          width: 100%;
        }
      }

      /* Estilos para tabela de resumo */
      .table-container {
        overflow-x: auto;
      }

      table {
        width: 100%;
        border-collapse: collapse;
      }

      th, td {
        padding: 0.75rem;
        text-align: left;
        border-bottom: 1px solid var(--border-color);
      }

      th {
        background-color: rgba(93, 92, 222, 0.1);
        font-weight: 600;
      }

      tr:hover {
        background-color: rgba(0, 0, 0, 0.02);
      }

      /* Fixar sticky tab bar no mobile */
      @media (max-width: 768px) {
        .sticky-tabs {
          position: sticky;
          top: 0;
          background-color: var(--bg-color);
          z-index: 10;
          padding-top: 0.5rem;
        }
      }

      /* Animações */
      @keyframes fadeIn {
        from { opacity: 0; }
        to { opacity: 1; }
      }

      .fade-in {
        animation: fadeIn 0.3s ease forwards;
      }
      
      /* Modal */
      .modal-overlay {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1000;
      }
      
      .modal-content {
        background-color: var(--card-bg);
        padding: 1.5rem;
        border-radius: 0.5rem;
        max-width: 90%;
        max-height: 90%;
        overflow-y: auto;
        width: 500px;
        position: relative;
      }
      
      .modal-close {
        position: absolute;
        top: 0.5rem;
        right: 0.5rem;
        font-size: 1.5rem;
        cursor: pointer;
        background: none;
        border: none;
        color: var(--text-color);
      }
      
      /* Lista de pacientes */
      .patient-card {
        padding: 1rem;
        border: 1px solid var(--border-color);
        border-radius: 0.25rem;
        margin-bottom: 0.5rem;
        cursor: pointer;
        transition: background-color 0.2s;
      }
      
      .patient-card:hover {
        background-color: rgba(93, 92, 222, 0.1);
      }
      
      .patient-card.selected {
        background-color: rgba(93, 92, 222, 0.2);
        border-color: var(--primary-color);
      }
      
      .patient-actions {
        display: flex;
        gap: 0.5rem;
        margin-top: 0.5rem;
      }
      
      .patient-actions button {
        padding: 0.25rem 0.5rem;
        font-size: 0.875rem;
      }
      
      /* iOS específico */
      input[type="datetime-local"],
      input[type="date"] {
        -webkit-appearance: none;
        appearance: none;
      }
      
      /* Data picker fixes para iOS */
      @supports (-webkit-touch-callout: none) {
        input[type="date"],
        input[type="datetime-local"] {
          display: block;
          position: relative;
        }
      }
      
      /* File dropzone */
      .dropzone {
        border: 2px dashed var(--border-color);
        border-radius: 0.5rem;
        padding: 2rem;
        text-align: center;
        cursor: pointer;
        margin-bottom: 1rem;
      }
      
      .dropzone.active {
        border-color: var(--primary-color);
        background-color: rgba(93, 92, 222, 0.1);
      }
      
      /* Badge */
      .badge {
        display: inline-block;
        padding: 0.25rem 0.5rem;
        font-size: 0.75rem;
        font-weight: 600;
        border-radius: 0.25rem;
        margin-left: 0.5rem;
      }
      
      .badge-primary {
        background-color: var(--primary-color);
        color: white;
      }
      
      .badge-warning {
        background-color: var(--warning-color);
        color: #212529;
      }
      
      .badge-danger {
        background-color: var(--danger-color);
        color: white;
      }
      
      /* JSON Viewer */
      #jsonContent {
        font-family: monospace;
        overflow-x: auto;
        white-space: pre-wrap;
        word-wrap: break-word;
        max-height: 60vh;
      }
      
      .json-viewer {
        width: 90vw;
        max-width: 800px;
      }
      
      .json-key {
        color: #a6e22e;
      }
      
      .json-string {
        color: #fd971f;
      }
      
      .json-number {
        color: #66d9ef;
      }
      
      .json-boolean {
        color: #ae81ff;
      }
      
      .json-null {
        color: #f92672;
      }
    </style>
</head>
<body>
  <div class="container">
    <header class="text-center my-6">
      <h1 class="text-2xl font-bold">Round Matinal - UTI</h1>
      <p class="text-sm text-gray-600 dark:text-gray-400">Sistema de avaliação e coleta de dados</p>
    </header>

    <!-- Botões do menu principal -->
    <div class="card" id="mainMenu">
      <div class="flex-container">
        <div>
          <button type="button" id="newPatientBtn" class="btn btn-primary w-full">Novo Paciente</button>
        </div>
        <div>
          <button type="button" id="loadPatientBtn" class="btn btn-primary w-full">Carregar Paciente</button>
        </div>
      </div>
      <div id="syncStatus" class="text-center mt-4 text-sm">
        <p>Último backup: <span id="lastSyncTime">Nunca</span></p>
      </div>
      <div class="flex-container mt-4">
        <div>
          <button type="button" id="exportDataBtn" class="btn btn-warning w-full">Exportar Banco de Dados</button>
        </div>
        <div>
          <button type="button" id="importDataBtn" class="btn btn-warning w-full">Importar Banco de Dados</button>
        </div>
      </div>
      <div class="flex-container mt-4">
        <div>
          <button type="button" id="viewJsonBtn" class="btn btn-primary w-full">Visualizar Arquivo JSON</button>
        </div>
      </div>
    </div>

    <!-- Lista de pacientes para carregar -->
    <div id="patientListModal" class="modal-overlay hidden">
      <div class="modal-content">
        <button class="modal-close" id="closePatientList">&times;</button>
        <h2 class="text-xl font-semibold mb-4">Selecione um Paciente</h2>
        <div class="form-group">
          <input type="text" id="patientSearch" class="form-control" placeholder="Buscar paciente...">
        </div>
        <div id="patientList" class="mt-4">
          <!-- Lista de pacientes será preenchida dinamicamente -->
          <div class="spinner" id="patientListLoading"></div>
        </div>
      </div>
    </div>
    
    <!-- Modal para importar dados -->
    <div id="importModal" class="modal-overlay hidden">
      <div class="modal-content">
        <button class="modal-close" id="closeImportModal">&times;</button>
        <h2 class="text-xl font-semibold mb-4">Importar Banco de Dados</h2>
        <div class="alert alert-warning">
          <p>Atenção: Importar um banco de dados substituirá todos os dados existentes.</p>
        </div>
        <div class="dropzone" id="dropzone">
          <p>Arraste o arquivo de backup aqui ou clique para selecionar</p>
          <input type="file" id="fileInput" accept=".json" class="hidden">
        </div>
        <div class="btn-group">
          <button type="button" id="confirmImport" class="btn btn-danger" disabled>Importar e Substituir Dados</button>
          <button type="button" id="cancelImport" class="btn btn-primary">Cancelar</button>
        </div>
      </div>
    </div>
    
    <!-- Modal para visualizar JSON -->
    <div id="jsonViewerModal" class="modal-overlay hidden">
      <div class="modal-content json-viewer">
        <button class="modal-close" id="closeJsonViewer">&times;</button>
        <h2 class="text-xl font-semibold mb-4">Visualizador de JSON</h2>
        <div class="dropzone" id="jsonDropzone">
          <p>Arraste um arquivo JSON aqui ou clique para selecionar</p>
          <input type="file" id="jsonFileInput" accept=".json" class="hidden">
        </div>
        <div id="jsonContent" class="mt-4 hidden p-4 rounded bg-gray-50 dark:bg-gray-800">
          <!-- O conteúdo do JSON será exibido aqui -->
        </div>
      </div>
    </div>

    <div class="tabs sticky-tabs hidden" id="formTabs">
      <div class="tab active" data-tab="identificacao">Identificação</div>
      <div class="tab" data-tab="dispositivos">Dispositivos</div>
      <div class="tab" data-tab="ventilacao">Ventilação</div>
      <div class="tab" data-tab="medicacoes">Medicações</div>
      <div class="tab" data-tab="outros">Outros Parâmetros</div>
      <div class="tab" data-tab="resumo">Resumo</div>
    </div>

    <form id="roundMatinalForm" class="hidden">
      <!-- Identificação do Paciente -->
      <div id="identificacao" class="tab-content active">
        <div class="card">
          <h2 class="text-xl font-semibold">Identificação do Paciente</h2>
          
          <div class="form-group">
            <label for="nomePaciente" class="form-label">Nome:</label>
            <input type="text" id="nomePaciente" name="nomePaciente" class="form-control" placeholder="Digite o nome do paciente" required>
          </div>

          <div class="flex-container">
            <div class="form-group">
              <label for="registroHospitalar" class="form-label">Registro Hospitalar:</label>
              <input type="text" id="registroHospitalar" name="registroHospitalar" class="form-control" placeholder="Digite o registro hospitalar" required>
            </div>
            <div class="form-group">
              <label for="leito" class="form-label">Leito:</label>
              <select id="leito" name="leito" class="form-control" required>
                <option value="" disabled selected>Selecione o leito</option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
                <option value="9">9</option>
                <option value="10">10</option>
              </select>
            </div>
          </div>

          <div class="flex-container">
            <div class="form-group">
              <label for="dataNascimento" class="form-label">Data de Nascimento:</label>
              <input type="date" id="dataNascimento" name="dataNascimento" class="form-control" required>
            </div>
            <div class="form-group">
              <label for="idade" class="form-label">Idade:</label>
              <input type="text" id="idade" name="idade" class="form-control" readonly placeholder="Calculado automaticamente">
            </div>
            <div class="form-group">
              <label for="peso" class="form-label">Peso (kg):</label>
              <input type="number" id="peso" name="peso" class="form-control" step="0.1" min="0" placeholder="Informe o peso em kg" required>
            </div>
          </div>

          <div class="flex-container">
            <div class="form-group">
              <label for="dataInternacao" class="form-label">Data de Internação:</label>
              <input type="date" id="dataInternacao" name="dataInternacao" class="form-control" required>
            </div>
            <div class="form-group">
              <label for="dataPreenchimento" class="form-label">Data do Preenchimento:</label>
              <input type="date" id="dataPreenchimento" name="dataPreenchimento" class="form-control" required>
            </div>
            <div class="form-group">
              <label for="tempoInternacao" class="form-label">Tempo de Internação:</label>
              <input type="text" id="tempoInternacao" name="tempoInternacao" class="form-control" readonly placeholder="Calculado automaticamente">
            </div>
          </div>

          <div class="btn-group justify-end">
            <button type="button" class="btn btn-primary" id="nextToDispositivos">Próximo</button>
          </div>
        </div>
      </div>

      <!-- Dispositivos (Cateteres e Sondas) -->
      <div id="dispositivos" class="tab-content">
        <div class="card">
          <h2 class="text-xl font-semibold">Uso de Cateteres</h2>
          <div id="cateteresContainer">
            <!-- Entradas de cateteres serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addCateter" class="btn btn-primary">Adicionar Cateter</button>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Uso de Sondas</h2>
          <div id="sondasContainer">
            <!-- As sondas serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addSonda" class="btn btn-primary">Adicionar Sonda</button>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Uso de Drogas Vasoativas</h2>
          <div id="drogasContainer">
            <!-- Entradas de drogas serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addDroga" class="btn btn-primary">Adicionar Droga</button>
        </div>

        <div class="btn-group justify-between">
          <button type="button" class="btn btn-primary" id="backToIdentificacao">Anterior</button>
          <button type="button" class="btn btn-primary" id="nextToVentilacao">Próximo</button>
        </div>
      </div>

      <!-- Ventilação Mecânica -->
      <div id="ventilacao" class="tab-content">
        <div class="card">
          <h2 class="text-xl font-semibold">Ventilação Mecânica</h2>

          <div class="form-group">
            <label for="pacienteIntubado" class="form-label">Paciente Intubado?</label>
            <select id="pacienteIntubado" name="pacienteIntubado" class="form-control" required>
              <option value="" disabled selected>Selecione uma opção</option>
              <option value="Sim">Sim</option>
              <option value="Não">Não</option>
            </select>
          </div>

          <div id="intubacaoDetails" class="hidden">
            <div class="flex-container">
              <div class="form-group">
                <label for="dataIntubacao" class="form-label">Data de Intubação:</label>
                <input type="datetime-local" id="dataIntubacao" name="dataIntubacao" class="form-control">
              </div>
              <div class="form-group">
                <label for="tempoIntubacao" class="form-label">Tempo de Intubação:</label>
                <div class="status-container">
                  <input type="text" id="tempoIntubacao" name="tempoIntubacao" class="form-control" readonly placeholder="Será calculado automaticamente">
                  <span id="statusIntubacao" class="status-indicator"></span>
                </div>
              </div>
            </div>

            <div class="form-group">
              <label for="modoVentilacao" class="form-label">Modo de Ventilação:</label>
              <select id="modoVentilacao" name="modoVentilacao" class="form-control">
                <option value="" disabled selected>Selecione um modo</option>
                <option value="PCV">PCV</option>
                <option value="VCV">VCV</option>
                <option value="PSV">PSV</option>
                <option value="Outros">Outros</option>
              </select>
            </div>

            <div id="ventilacaoParametros" class="hidden">
              <div class="flex-container">
                <div class="form-group">
                  <label for="fio2" class="form-label">FiO2 (%):</label>
                  <input type="number" id="fio2" name="fio2" class="form-control" min="21" max="100" placeholder="21-100">
                </div>
                <div class="form-group">
                  <label for="fr" class="form-label">FR (irpm):</label>
                  <input type="number" id="fr" name="fr" class="form-control" min="0" placeholder="Frequência respiratória">
                </div>
              </div>

              <div class="flex-container">
                <div class="form-group">
                  <label for="pinsp" class="form-label">Pinsp (cmH2O):</label>
                  <input type="number" id="pinsp" name="pinsp" class="form-control" placeholder="Pressão inspiratória">
                </div>
                <div class="form-group">
                  <label for="vc" class="form-label">VC (ml):</label>
                  <input type="number" id="vc" name="vc" class="form-control" placeholder="Volume corrente">
                </div>
              </div>

              <div class="flex-container">
                <div class="form-group">
                  <label for="volm" class="form-label">Vol/m (ml/kg):</label>
                  <input type="number" id="volm" name="volm" class="form-control" step="0.1" placeholder="Volume/min">
                </div>
                <div class="form-group">
                  <label for="peep" class="form-label">PEEP (cmH2O):</label>
                  <input type="number" id="peep" name="peep" class="form-control" placeholder="PEEP">
                </div>
              </div>

              <div class="flex-container">
                <div class="form-group">
                  <label for="ppico" class="form-label">Ppico (cmH2O):</label>
                  <input type="number" id="ppico" name="ppico" class="form-control" placeholder="Pressão de pico">
                </div>
                <div class="form-group">
                  <label for="pplato" class="form-label">Pplato (cmH2O):</label>
                  <input type="number" id="pplato" name="pplato" class="form-control" placeholder="Pressão de platô">
                </div>
              </div>
            </div>

            <div id="psvDetails" class="hidden">
              <div class="form-group">
                <label for="podeExtubar" class="form-label">Paciente Pode Extubar?</label>
                <select id="podeExtubar" name="podeExtubar" class="form-control">
                  <option value="" disabled selected>Selecione uma opção</option>
                  <option value="Sim">Sim</option>
                  <option value="Não">Não</option>
                </select>
              </div>
            </div>

            <div id="traqueostomiaContainer" class="hidden">
              <div class="alert alert-warning">
                <p>Paciente com mais de 5 dias de intubação. Considerar traqueostomia.</p>
              </div>
              <div class="checkbox-container">
                <input type="checkbox" id="realizouTraqueostomia" name="realizouTraqueostomia">
                <label for="realizouTraqueostomia">Realizou Traqueostomia?</label>
              </div>
              <div id="dataTraqueostomiaContainer" class="hidden">
                <div class="form-group">
                  <label for="dataTraqueostomia" class="form-label">Data da Traqueostomia:</label>
                  <input type="datetime-local" id="dataTraqueostomia" name="dataTraqueostomia" class="form-control">
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="btn-group justify-between">
          <button type="button" class="btn btn-primary" id="backToDispositivos">Anterior</button>
          <button type="button" class="btn btn-primary" id="nextToMedicacoes">Próximo</button>
        </div>
      </div>

      <!-- Medicações -->
      <div id="medicacoes" class="tab-content">
        <div class="card">
          <h2 class="text-xl font-semibold">Sedação</h2>
          <div id="sedacaoContainer">
            <!-- Entradas de sedação serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addSedacao" class="btn btn-primary">Adicionar Sedação</button>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Analgesia</h2>
          <div id="analgesiaContainer">
            <!-- Entradas de analgesia serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addAnalgesia" class="btn btn-primary">Adicionar Analgesia</button>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Uso de Antibióticos</h2>
          <div id="antibioticosContainer">
            <!-- Entradas de antibióticos serão adicionadas dinamicamente -->
          </div>
          <button type="button" id="addAntibiotico" class="btn btn-primary">Adicionar Antibiótico</button>
        </div>

        <div class="btn-group justify-between">
          <button type="button" class="btn btn-primary" id="backToVentilacao">Anterior</button>
          <button type="button" class="btn btn-primary" id="nextToOutros">Próximo</button>
        </div>
      </div>

      <!-- Outros Parâmetros -->
      <div id="outros" class="tab-content">
        <div class="card">
          <h2 class="text-xl font-semibold">Alimentação</h2>
          <div class="form-group">
            <label for="viaAlimentacao" class="form-label">Via de Alimentação:</label>
            <select id="viaAlimentacao" name="viaAlimentacao" class="form-control" required>
              <option value="" disabled selected>Selecione uma opção</option>
              <option value="VO">VO</option>
              <option value="SNG">SNG</option>
              <option value="SNE">SNE</option>
              <option value="Gastrostomia">Gastrostomia</option>
              <option value="Jejunostomia">Jejunostomia</option>
              <option value="Jejum">Jejum</option>
            </select>
          </div>

          <div id="quantidadeContainer" class="hidden">
            <div class="form-group">
              <label for="quantidadeDiaria" class="form-label">Quantidade Diária (ml):</label>
              <input type="number" id="quantidadeDiaria" name="quantidadeDiaria" class="form-control" placeholder="Informe a quantidade diária">
            </div>
          </div>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Trânsito Intestinal</h2>
          <div class="form-group">
            <label for="transitoIntestinal" class="form-label">Trânsito Intestinal:</label>
            <select id="transitoIntestinal" name="transitoIntestinal" class="form-control" required>
              <option value="" disabled selected>Selecione uma opção</option>
              <option value="Normal">Normal</option>
              <option value="Constipado">Constipado</option>
              <option value="Diarreia">Diarreia</option>
              <option value="Ausente">Ausente</option>
            </select>
          </div>

          <div class="flex-container">
            <div class="form-group">
              <label for="dataUltimaEvacuacao" class="form-label">Data da Última Evacuação:</label>
              <input type="datetime-local" id="dataUltimaEvacuacao" name="dataUltimaEvacuacao" class="form-control">
            </div>
            <div class="form-group">
              <label for="tempoDesdeEvacuacao" class="form-label">Tempo desde Última Evacuação:</label>
              <input type="text" id="tempoDesdeEvacuacao" name="tempoDesdeEvacuacao" class="form-control" readonly placeholder="Será calculado automaticamente">
            </div>
          </div>
        </div>

        <div class="flex-container">
          <div class="card">
            <h2 class="text-xl font-semibold">Trombofilaxia</h2>
            <div class="form-group">
              <label for="usoTrombofilaxia" class="form-label">Uso de Trombofilaxia:</label>
              <select id="usoTrombofilaxia" name="usoTrombofilaxia" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="Sim">Sim</option>
                <option value="Não">Não</option>
              </select>
            </div>

            <div id="trombofilaxiaDetails" class="hidden">
              <div class="form-group">
                <label for="tipoTrombofilaxia" class="form-label">Tipo de Trombofilaxia:</label>
                <select id="tipoTrombofilaxia" name="tipoTrombofilaxia" class="form-control">
                  <option value="" disabled selected>Selecione um tipo</option>
                  <option value="Heparina">Heparina</option>
                  <option value="Enoxaparina">Enoxaparina</option>
                  <option value="Oral">Oral</option>
                  <option value="Outros">Outros</option>
                </select>
              </div>
            </div>
          </div>

          <div class="card">
            <h2 class="text-xl font-semibold">Proteção Gástrica</h2>
            <div class="form-group">
              <label for="usoProtecaoGastrica" class="form-label">Uso de Proteção Gástrica:</label>
              <select id="usoProtecaoGastrica" name="usoProtecaoGastrica" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="Sim">Sim</option>
                <option value="Não">Não</option>
              </select>
            </div>

            <div id="protecaoGastricaDetails" class="hidden">
              <div class="form-group">
                <label for="tipoProtecaoGastrica" class="form-label">Tipo de Proteção Gástrica:</label>
                <select id="tipoProtecaoGastrica" name="tipoProtecaoGastrica" class="form-control">
                  <option value="" disabled selected>Selecione uma opção</option>
                  <option value="Omeprazol">Omeprazol</option>
                  <option value="Pantoprazol">Pantoprazol</option>
                  <option value="Ranitidina">Ranitidina</option>
                  <option value="Outros">Outros</option>
                </select>
              </div>
            </div>
          </div>
        </div>

        <div class="flex-container">
          <div class="card">
            <h2 class="text-xl font-semibold">Controle Glicêmico</h2>
            <div class="form-group">
              <label for="glicemiaAtual" class="form-label">Glicemia Atual (mg/dL):</label>
              <input type="number" id="glicemiaAtual" name="glicemiaAtual" class="form-control" placeholder="Informe a glicemia atual">
            </div>

            <div class="form-group">
              <label for="controleGlicemico" class="form-label">Controle Glicêmico:</label>
              <select id="controleGlicemico" name="controleGlicemico" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="Insulina NPH">Insulina NPH</option>
                <option value="Insulina Regular">Insulina Regular</option>
                <option value="Nenhum">Nenhum</option>
              </select>
            </div>
          </div>

          <div class="card">
            <h2 class="text-xl font-semibold">Cabeceira e Conforto</h2>
            <div class="form-group">
              <label for="elevacaoCabeceira" class="form-label">Elevação da Cabeceira:</label>
              <select id="elevacaoCabeceira" name="elevacaoCabeceira" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="0 graus">0 graus</option>
                <option value="30 graus">30 graus</option>
                <option value="45 graus">45 graus</option>
                <option value="Acima de 45 graus">Acima de 45 graus</option>
              </select>
            </div>

            <div class="form-group">
              <label for="nivelConforto" class="form-label">Nível de Conforto do Paciente:</label>
              <select id="nivelConforto" name="nivelConforto" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="Confortável">Confortável</option>
                <option value="Moderadamente desconfortável">Moderadamente desconfortável</option>
                <option value="Muito desconfortável">Muito desconfortável</option>
              </select>
            </div>
          </div>
        </div>

        <div class="card">
          <h2 class="text-xl font-semibold">Pendências / Condutas</h2>
          <div class="form-group">
            <label for="pendenciasCondutas" class="form-label">Observações:</label>
            <textarea id="pendenciasCondutas" name="pendenciasCondutas" class="form-control" rows="5" placeholder="Insira aqui as pendências ou condutas do paciente"></textarea>
          </div>
        </div>

        <div class="btn-group justify-between">
          <button type="button" class="btn btn-primary" id="backToMedicacoes">Anterior</button>
          <button type="button" class="btn btn-primary" id="nextToResumo">Gerar Resumo</button>
        </div>
      </div>

      <!-- Resumo -->
      <div id="resumo" class="tab-content">
        <div class="card">
          <h2 class="text-xl font-semibold">Resumo da Avaliação</h2>
          <div id="resumoContent" class="mt-4">
            <!-- O conteúdo do resumo será gerado dinamicamente -->
            <div id="loadingResumo" class="spinner"></div>
          </div>
        </div>

        <div class="btn-group justify-between">
          <button type="button" class="btn btn-primary" id="backToOutros">Voltar</button>
          <button type="button" class="btn btn-success" id="saveData">Salvar Dados</button>
          <button type="button" class="btn btn-primary" id="exportarCSV">Exportar para CSV</button>
          <button type="button" class="btn btn-primary" id="exportarPDF">Exportar em PDF</button>
          <button type="button" class="btn btn-danger" id="clearForm">Limpar Formulário</button>
        </div>
      </div>
    </form>
  </div>

  <div id="toast" class="toast">Mensagem de notificação</div>

  <script src="https://cdn.jsdelivr.net/npm/flowbite@1.6.5/dist/flowbite.min.js"></script>
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      // ============ INICIALIZAÇÃO DO BANCO DE DADOS ============
      let db;
      const DB_NAME = 'RoundMatinalUTI';
      const DB_VERSION = 1;
      const PATIENTS_STORE = 'patients';
      const SETTINGS_STORE = 'settings';

      // Estado da aplicação
      let currentPatientId = null;
      let formState = {
        lastSaved: null,
        isDirty: false,
        isNewPatient: true
      };

      // Inicializar o IndexedDB
      function initDatabase() {
        return new Promise((resolve, reject) => {
          const request = indexedDB.open(DB_NAME, DB_VERSION);
          
          request.onerror = event => {
            console.error("Erro ao abrir banco de dados:", event.target.error);
            showToast("Erro ao acessar o banco de dados. Alguns recursos podem estar indisponíveis.", 5000);
            reject(event.target.error);
          };
          
          request.onupgradeneeded = event => {
            const db = event.target.result;
            
            // Criar object store para pacientes se não existir
            if (!db.objectStoreNames.contains(PATIENTS_STORE)) {
              const patientsStore = db.createObjectStore(PATIENTS_STORE, { keyPath: 'id' });
              patientsStore.createIndex('by_name', 'nomePaciente', { unique: false });
              patientsStore.createIndex('by_register', 'registroHospitalar', { unique: false });
              patientsStore.createIndex('by_updated', 'updatedAt', { unique: false });
            }
            
            // Criar object store para configurações se não existir
            if (!db.objectStoreNames.contains(SETTINGS_STORE)) {
              const settingsStore = db.createObjectStore(SETTINGS_STORE, { keyPath: 'id' });
            }
          };
          
          request.onsuccess = event => {
            db = event.target.result;
            console.log("Banco de dados inicializado com sucesso");
            
            // Verificar último backup
            checkLastBackup();
            
            resolve(db);
          };
        });
      }

      // Verificar a data do último backup
      function checkLastBackup() {
        const transaction = db.transaction([SETTINGS_STORE], 'readonly');
        const store = transaction.objectStore(SETTINGS_STORE);
        const request = store.get('backupSettings');
        
        request.onsuccess = event => {
          const result = event.target.result;
          const lastSyncTimeElement = document.getElementById('lastSyncTime');
          
          if (result && result.lastBackup) {
            const backupDate = new Date(result.lastBackup);
            lastSyncTimeElement.textContent = formatDate(backupDate, true);
            
            // Verificar se o backup está desatualizado (mais de 7 dias)
            const oneWeekAgo = new Date();
            oneWeekAgo.setDate(oneWeekAgo.getDate() - 7);
            
            if (backupDate < oneWeekAgo) {
              lastSyncTimeElement.classList.add('text-danger');
              lastSyncTimeElement.textContent += " (Desatualizado)";
            }
          } else {
            lastSyncTimeElement.textContent = "Nunca";
          }
        };
        
        request.onerror = event => {
          console.error("Erro ao verificar último backup:", event.target.error);
        };
      }

      // Salvar a data do último backup
      function updateLastBackup() {
        const transaction = db.transaction([SETTINGS_STORE], 'readwrite');
        const store = transaction.objectStore(SETTINGS_STORE);
        
        const backup = {
          id: 'backupSettings',
          lastBackup: new Date().toISOString()
        };
        
        store.put(backup);
        
        transaction.oncomplete = () => {
          checkLastBackup();
        };
      }
      
      // ============ VISUALIZADOR DE JSON ============
      
      // Configurar modal do visualizador de JSON
      const jsonViewerModal = document.getElementById('jsonViewerModal');
      const closeJsonViewer = document.getElementById('closeJsonViewer');
      const jsonDropzone = document.getElementById('jsonDropzone');
      const jsonFileInput = document.getElementById('jsonFileInput');
      const jsonContent = document.getElementById('jsonContent');
      
      // Botão para abrir o visualizador de JSON
      document.getElementById('viewJsonBtn').addEventListener('click', () => {
        jsonViewerModal.classList.remove('hidden');
        jsonContent.classList.add('hidden');
        jsonContent.innerHTML = '';
      });
      
      // Fechar o visualizador de JSON
      closeJsonViewer.addEventListener('click', () => {
        jsonViewerModal.classList.add('hidden');
      });
      
      // Configurar dropzone para o visualizador de JSON
      jsonDropzone.addEventListener('click', () => {
        jsonFileInput.click();
      });
      
      jsonDropzone.addEventListener('dragover', (e) => {
        e.preventDefault();
        jsonDropzone.classList.add('active');
      });
      
      jsonDropzone.addEventListener('dragleave', () => {
        jsonDropzone.classList.remove('active');
      });
      
      jsonDropzone.addEventListener('drop', (e) => {
        e.preventDefault();
        jsonDropzone.classList.remove('active');
        
        if (e.dataTransfer.files.length) {
          jsonFileInput.files = e.dataTransfer.files;
          readJsonFile();
        }
      });
      
      jsonFileInput.addEventListener('change', readJsonFile);
      
      // Função para ler e exibir o arquivo JSON
      function readJsonFile() {
        const file = jsonFileInput.files[0];
        
        if (!file) {
          showToast('Selecione um arquivo JSON', 3000);
          return;
        }
        
        if (file.type !== 'application/json' && !file.name.endsWith('.json')) {
          showToast('Selecione um arquivo JSON válido', 3000);
          jsonFileInput.value = '';
          return;
        }
        
        const reader = new FileReader();
        
        reader.onload = (e) => {
          try {
            const json = JSON.parse(e.target.result);
            displayJson(json);
          } catch (error) {
            showToast('Erro ao processar o JSON: ' + error.message, 5000);
            jsonContent.classList.add('hidden');
          }
        };
        
        reader.onerror = () => {
          showToast('Erro ao ler o arquivo', 3000);
          jsonContent.classList.add('hidden');
        };
        
        reader.readAsText(file);
      }
      
      // Função para exibir o JSON formatado
      function displayJson(json) {
        // Formatação bonita do JSON com indentação
        const jsonString = JSON.stringify(json, null, 2);
        const coloredJson = syntaxHighlight(jsonString);
        
        jsonContent.innerHTML = coloredJson;
        jsonContent.classList.remove('hidden');
        jsonDropzone.textContent = 'Arquivo carregado. Arraste outro arquivo para substituir.';
      }
      
      // Função para destacar a sintaxe do JSON
      function syntaxHighlight(json) {
        json = json.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
        return json.replace(/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?)/g, function (match) {
          let cls = 'json-number';
          if (/^"/.test(match)) {
            if (/:$/.test(match)) {
              cls = 'json-key';
              match = match.replace(/"(.*)":/g, '<span class="json-key">"$1"</span>:');
              return match;
            } else {
              cls = 'json-string';
            }
          } else if (/true|false/.test(match)) {
            cls = 'json-boolean';
          } else if (/null/.test(match)) {
            cls = 'json-null';
          }
          return '<span class="' + cls + '">' + match + '</span>';
        });
      }

      // ============ FUNÇÕES PRINCIPAIS DO FORMULÁRIO ============
      
      // Elementos DOM para as abas
      const tabs = document.querySelectorAll('.tab');
      const tabContents = document.querySelectorAll('.tab-content');
      const mainMenu = document.getElementById('mainMenu');
      const formTabs = document.getElementById('formTabs');
      const roundForm = document.getElementById('roundMatinalForm');

      // Função para mostrar uma aba específica
      function showTab(tabId) {
        tabContents.forEach(content => {
          content.classList.remove('active');
        });
        
        tabs.forEach(tab => {
          tab.classList.remove('active');
        });
        
        document.getElementById(tabId).classList.add('active');
        document.querySelector(`.tab[data-tab="${tabId}"]`).classList.add('active');
        
        // Scroll para o topo quando trocar de aba
        window.scrollTo(0, 0);
      }

      // Configurar navegação entre abas
      tabs.forEach(tab => {
        tab.addEventListener('click', () => {
          const tabId = tab.getAttribute('data-tab');
          showTab(tabId);
        });
      });

      // Botões de navegação entre abas
      document.getElementById('nextToDispositivos').addEventListener('click', () => showTab('dispositivos'));
      document.getElementById('backToIdentificacao').addEventListener('click', () => showTab('identificacao'));
      document.getElementById('nextToVentilacao').addEventListener('click', () => showTab('ventilacao'));
      document.getElementById('backToDispositivos').addEventListener('click', () => showTab('dispositivos'));
      document.getElementById('nextToMedicacoes').addEventListener('click', () => showTab('medicacoes'));
      document.getElementById('backToVentilacao').addEventListener('click', () => showTab('ventilacao'));
      document.getElementById('nextToOutros').addEventListener('click', () => showTab('outros'));
      document.getElementById('backToMedicacoes').addEventListener('click', () => showTab('medicacoes'));
      document.getElementById('nextToResumo').addEventListener('click', () => {
        showTab('resumo');
        generateSummary();
      });
      document.getElementById('backToOutros').addEventListener('click', () => showTab('outros'));

      // Elementos DOM para os campos do formulário
      const elements = {
        // Identificação do Paciente
        nomePaciente: document.getElementById('nomePaciente'),
        registroHospitalar: document.getElementById('registroHospitalar'),
        leito: document.getElementById('leito'),
        dataNascimento: document.getElementById('dataNascimento'),
        idade: document.getElementById('idade'),
        peso: document.getElementById('peso'),
        dataInternacao: document.getElementById('dataInternacao'),
        dataPreenchimento: document.getElementById('dataPreenchimento'),
        tempoInternacao: document.getElementById('tempoInternacao'),

        // Ventilação Mecânica
        pacienteIntubado: document.getElementById('pacienteIntubado'),
        intubacaoDetails: document.getElementById('intubacaoDetails'),
        dataIntubacao: document.getElementById('dataIntubacao'),
        tempoIntubacao: document.getElementById('tempoIntubacao'),
        statusIntubacao: document.getElementById('statusIntubacao'),
        modoVentilacao: document.getElementById('modoVentilacao'),
        ventilacaoParametros: document.getElementById('ventilacaoParametros'),
        fio2: document.getElementById('fio2'),
        fr: document.getElementById('fr'),
        pinsp: document.getElementById('pinsp'),
        vc: document.getElementById('vc'),
        volm: document.getElementById('volm'),
        peep: document.getElementById('peep'),
        ppico: document.getElementById('ppico'),
        pplato: document.getElementById('pplato'),
        psvDetails: document.getElementById('psvDetails'),
        traqueostomiaContainer: document.getElementById('traqueostomiaContainer'),
        realizouTraqueostomia: document.getElementById('realizouTraqueostomia'),
        dataTraqueostomiaContainer: document.getElementById('dataTraqueostomiaContainer'),
        dataTraqueostomia: document.getElementById('dataTraqueostomia'),

        // Alimentação
        viaAlimentacao: document.getElementById('viaAlimentacao'),
        quantidadeContainer: document.getElementById('quantidadeContainer'),
        quantidadeDiaria: document.getElementById('quantidadeDiaria'),

        // Trânsito Intestinal
        transitoIntestinal: document.getElementById('transitoIntestinal'),
        dataUltimaEvacuacao: document.getElementById('dataUltimaEvacuacao'),
        tempoDesdeEvacuacao: document.getElementById('tempoDesdeEvacuacao'),

        // Containers
        cateteresContainer: document.getElementById('cateteresContainer'),
        sondasContainer: document.getElementById('sondasContainer'),
        drogasContainer: document.getElementById('drogasContainer'),
        sedacaoContainer: document.getElementById('sedacaoContainer'),
        analgesiaContainer: document.getElementById('analgesiaContainer'),
        antibioticosContainer: document.getElementById('antibioticosContainer'),

        // Proteção Gástrica e Trombofilaxia
        usoProtecaoGastrica: document.getElementById('usoProtecaoGastrica'),
        tipoProtecaoGastrica: document.getElementById('tipoProtecaoGastrica'),
        protecaoGastricaDetails: document.getElementById('protecaoGastricaDetails'),
        usoTrombofilaxia: document.getElementById('usoTrombofilaxia'),
        tipoTrombofilaxia: document.getElementById('tipoTrombofilaxia'),
        trombofilaxiaDetails: document.getElementById('trombofilaxiaDetails'),

        // Controle Glicêmico
        glicemiaAtual: document.getElementById('glicemiaAtual'),
        controleGlicemico: document.getElementById('controleGlicemico'),

        // Cabeceira e Conforto
        elevacaoCabeceira: document.getElementById('elevacaoCabeceira'),
        nivelConforto: document.getElementById('nivelConforto'),
        
        // Pendências/Condutas
        pendenciasCondutas: document.getElementById('pendenciasCondutas'),
        
        // Botões
        saveData: document.getElementById('saveData'),
        exportarCSV: document.getElementById('exportarCSV'),
        exportarPDF: document.getElementById('exportarPDF'),
        clearForm: document.getElementById('clearForm')
      };

      // Inicializar menu principal e botões
      document.getElementById('newPatientBtn').addEventListener('click', startNewPatient);
      document.getElementById('loadPatientBtn').addEventListener('click', showPatientList);
      document.getElementById('exportDataBtn').addEventListener('click', exportDatabase);
      document.getElementById('importDataBtn').addEventListener('click', showImportModal);
      
      // Configurar modal de importação
      document.getElementById('closeImportModal').addEventListener('click', () => {
        document.getElementById('importModal').classList.add('hidden');
      });
      document.getElementById('cancelImport').addEventListener('click', () => {
        document.getElementById('importModal').classList.add('hidden');
      });
      document.getElementById('confirmImport').addEventListener('click', importDatabase);
      
      // Configurar dropzone para importação
      const dropzone = document.getElementById('dropzone');
      const fileInput = document.getElementById('fileInput');
      
      dropzone.addEventListener('click', () => {
        fileInput.click();
      });
      
      dropzone.addEventListener('dragover', (e) => {
        e.preventDefault();
        dropzone.classList.add('active');
      });
      
      dropzone.addEventListener('dragleave', () => {
        dropzone.classList.remove('active');
      });
      
      dropzone.addEventListener('drop', (e) => {
        e.preventDefault();
        dropzone.classList.remove('active');
        
        if (e.dataTransfer.files.length) {
          fileInput.files = e.dataTransfer.files;
          validateImportFile();
        }
      });
      
      fileInput.addEventListener('change', validateImportFile);
      
      // Validar arquivo de importação
      function validateImportFile() {
        const file = fileInput.files[0];
        const confirmImportBtn = document.getElementById('confirmImport');
        
        if (file && file.type === 'application/json') {
          confirmImportBtn.removeAttribute('disabled');
          dropzone.textContent = `Arquivo selecionado: ${file.name}`;
        } else {
          confirmImportBtn.setAttribute('disabled', 'disabled');
          dropzone.textContent = 'Selecione um arquivo JSON válido';
          fileInput.value = '';
        }
      }
      
      // Configurar modal da lista de pacientes
      document.getElementById('closePatientList').addEventListener('click', () => {
        document.getElementById('patientListModal').classList.add('hidden');
      });
      
      // Filtro de busca para pacientes
      document.getElementById('patientSearch').addEventListener('input', function() {
        const searchTerm = this.value.toLowerCase();
        const patientCards = document.querySelectorAll('.patient-card');
        
        patientCards.forEach(card => {
          const patientName = card.getAttribute('data-name').toLowerCase();
          const patientRegister = card.getAttribute('data-register').toLowerCase();
          
          if (patientName.includes(searchTerm) || patientRegister.includes(searchTerm)) {
            card.style.display = 'block';
          } else {
            card.style.display = 'none';
          }
        });
      });
      
      // Iniciar novo paciente
      function startNewPatient() {
        resetForm();
        currentPatientId = generateId();
        formState.isNewPatient = true;
        formState.isDirty = false;
        
        // Esconder menu principal e mostrar formulário
        mainMenu.classList.add('hidden');
        formTabs.classList.remove('hidden');
        roundForm.classList.remove('hidden');
        
        // Configurar data de preenchimento para hoje
        const hoje = new Date();
        elements.dataPreenchimento.valueAsDate = hoje;
        
        // Mostrar primeira aba
        showTab('identificacao');
      }
      
      // Gerar ID único para novos pacientes
      function generateId() {
        return 'patient_' + Date.now() + '_' + Math.floor(Math.random() * 1000);
      }
      
      // Mostrar lista de pacientes para carregar
      function showPatientList() {
        const patientListModal = document.getElementById('patientListModal');
        const patientList = document.getElementById('patientList');
        const patientListLoading = document.getElementById('patientListLoading');
        
        // Limpar lista anterior e mostrar loading
        patientList.innerHTML = '';
        patientListLoading.style.display = 'block';
        patientListModal.classList.remove('hidden');
        
        // Buscar pacientes no banco de dados
        const transaction = db.transaction([PATIENTS_STORE], 'readonly');
        const store = transaction.objectStore(PATIENTS_STORE);
        const index = store.index('by_updated');
        const request = index.openCursor(null, 'prev');
        
        let patients = [];
        
        request.onsuccess = event => {
          const cursor = event.target.result;
          
          if (cursor) {
            patients.push(cursor.value);
            cursor.continue();
          } else {
            // Todos os pacientes foram carregados
            patientListLoading.style.display = 'none';
            
            if (patients.length === 0) {
              patientList.innerHTML = '<div class="alert alert-warning">Nenhum paciente encontrado.</div>';
              return;
            }
            
            // Criar cards para cada paciente
            patients.forEach(patient => {
              const card = document.createElement('div');
              card.className = 'patient-card';
              card.setAttribute('data-id', patient.id);
              card.setAttribute('data-name', patient.nomePaciente);
              card.setAttribute('data-register', patient.registroHospitalar);
              
              const updateDate = new Date(patient.updatedAt);
              const updateDateStr = formatDate(updateDate);
              
              card.innerHTML = `
                <div class="flex justify-between">
                  <div>
                    <strong>${patient.nomePaciente}</strong>
                    <div class="text-sm">Registro: ${patient.registroHospitalar || 'N/A'}</div>
                    <div class="text-sm">Leito: ${patient.leito || 'N/A'}</div>
                  </div>
                  <div class="text-sm text-gray-500">
                    Atualizado: ${updateDateStr}
                  </div>
                </div>
                <div class="patient-actions">
                  <button type="button" class="btn btn-primary load-patient-btn">Carregar</button>
                  <button type="button" class="btn btn-danger delete-patient-btn">Excluir</button>
                </div>
              `;
              
              // Adicionar evento para carregar paciente
              card.querySelector('.load-patient-btn').addEventListener('click', () => {
                loadPatient(patient.id);
                patientListModal.classList.add('hidden');
              });
              
              // Adicionar evento para excluir paciente
              card.querySelector('.delete-patient-btn').addEventListener('click', (e) => {
                e.stopPropagation();
                if (confirm(`Tem certeza que deseja excluir o paciente ${patient.nomePaciente}?`)) {
                  deletePatient(patient.id).then(() => {
                    card.remove();
                    if (patientList.children.length === 0) {
                      patientList.innerHTML = '<div class="alert alert-warning">Nenhum paciente encontrado.</div>';
                    }
                  });
                }
              });
              
              patientList.appendChild(card);
            });
          }
        };
        
        request.onerror = event => {
          console.error("Erro ao carregar lista de pacientes:", event.target.error);
          patientListLoading.style.display = 'none';
          patientList.innerHTML = '<div class="alert alert-danger">Erro ao carregar pacientes. Tente novamente.</div>';
        };
      }
      
      // Carregar paciente do banco de dados
      function loadPatient(patientId) {
        const transaction = db.transaction([PATIENTS_STORE], 'readonly');
        const store = transaction.objectStore(PATIENTS_STORE);
        const request = store.get(patientId);
        
        request.onsuccess = event => {
          const patient = event.target.result;
          
          if (patient) {
            currentPatientId = patientId;
            formState.isNewPatient = false;
            formState.isDirty = false;
            
            // Esconder menu principal e mostrar formulário
            mainMenu.classList.add('hidden');
            formTabs.classList.remove('hidden');
            roundForm.classList.remove('hidden');
            
            // Preencher o formulário com os dados do paciente
            fillFormWithPatient(patient);
            
            // Mostrar primeira aba
            showTab('identificacao');
          } else {
            showToast("Paciente não encontrado", 3000);
          }
        };
        
        request.onerror = event => {
          console.error("Erro ao carregar paciente:", event.target.error);
          showToast("Erro ao carregar paciente", 3000);
        };
      }
      
      // Excluir paciente do banco de dados
      function deletePatient(patientId) {
        return new Promise((resolve, reject) => {
          const transaction = db.transaction([PATIENTS_STORE], 'readwrite');
          const store = transaction.objectStore(PATIENTS_STORE);
          const request = store.delete(patientId);
          
          request.onsuccess = () => {
            showToast("Paciente excluído com sucesso", 3000);
            resolve();
          };
          
          request.onerror = event => {
            console.error("Erro ao excluir paciente:", event.target.error);
            showToast("Erro ao excluir paciente", 3000);
            reject(event.target.error);
          };
        });
      }
      
      // Preencher formulário com dados do paciente
      function fillFormWithPatient(patient) {
        resetForm();
        
        // Preencher campos de identificação
        elements.nomePaciente.value = patient.nomePaciente || '';
        elements.registroHospitalar.value = patient.registroHospitalar || '';
        elements.leito.value = patient.leito || '';
        elements.dataNascimento.value = patient.dataNascimento ? formatInputDate(patient.dataNascimento) : '';
        if (patient.dataNascimento) {
          calcularIdade();
        }
        elements.peso.value = patient.peso || '';
        elements.dataInternacao.value = patient.dataInternacao ? formatInputDate(patient.dataInternacao) : '';
        elements.dataPreenchimento.value = patient.dataPreenchimento ? formatInputDate(patient.dataPreenchimento) : '';
        elements.tempoInternacao.value = patient.tempoInternacao || '';
        
        // Preencher campos de ventilação mecânica
        if (elements.pacienteIntubado) {
          elements.pacienteIntubado.value = patient.pacienteIntubado || '';
          
          if (patient.pacienteIntubado === 'Sim') {
            elements.intubacaoDetails.classList.remove('hidden');
            
            if (elements.dataIntubacao && patient.dataIntubacao) {
              elements.dataIntubacao.value = formatInputDateTime(patient.dataIntubacao);
            }
            
            elements.tempoIntubacao.value = patient.tempoIntubacao || '';
            
            if (elements.modoVentilacao) {
              elements.modoVentilacao.value = patient.modoVentilacao || '';
              
              if (patient.modoVentilacao) {
                elements.ventilacaoParametros.classList.remove('hidden');
                
                // Preencher parâmetros de ventilação
                if (elements.fio2) elements.fio2.value = patient.fio2 || '';
                if (elements.fr) elements.fr.value = patient.fr || '';
                if (elements.pinsp) elements.pinsp.value = patient.pinsp || '';
                if (elements.vc) elements.vc.value = patient.vc || '';
                if (elements.volm) elements.volm.value = patient.volm || '';
                if (elements.peep) elements.peep.value = patient.peep || '';
                if (elements.ppico) elements.ppico.value = patient.ppico || '';
                if (elements.pplato) elements.pplato.value = patient.pplato || '';
              }
              
              if (patient.modoVentilacao === 'PSV' && elements.psvDetails) {
                elements.psvDetails.classList.remove('hidden');
                
                if (elements.podeExtubar) {
                  elements.podeExtubar.value = patient.podeExtubar || '';
                }
              }
            }
            
            if (elements.realizouTraqueostomia) {
              elements.realizouTraqueostomia.checked = patient.realizouTraqueostomia || false;
              
              if (patient.realizouTraqueostomia && elements.dataTraqueostomiaContainer) {
                elements.dataTraqueostomiaContainer.classList.remove('hidden');
                
                if (elements.dataTraqueostomia && patient.dataTraqueostomia) {
                  elements.dataTraqueostomia.value = formatInputDateTime(patient.dataTraqueostomia);
                }
              }
            }
          }
        }
        
        // Preencher campos de alimentação
        if (elements.viaAlimentacao) {
          elements.viaAlimentacao.value = patient.viaAlimentacao || '';
          
          if (['SNG', 'SNE', 'Gastrostomia', 'Jejunostomia'].includes(patient.viaAlimentacao) && elements.quantidadeContainer) {
            elements.quantidadeContainer.classList.remove('hidden');
            
            if (elements.quantidadeDiaria) {
              elements.quantidadeDiaria.value = patient.quantidadeDiaria || '';
            }
          }
        }
        
        // Preencher campos de trânsito intestinal
        if (elements.transitoIntestinal) {
          elements.transitoIntestinal.value = patient.transitoIntestinal || '';
        }
        
        if (elements.dataUltimaEvacuacao && patient.dataUltimaEvacuacao) {
          elements.dataUltimaEvacuacao.value = formatInputDateTime(patient.dataUltimaEvacuacao);
        }
        
        elements.tempoDesdeEvacuacao.value = patient.tempoDesdeEvacuacao || '';
        
        // Preencher proteção gástrica
        if (elements.usoProtecaoGastrica) {
          elements.usoProtecaoGastrica.value = patient.usoProtecaoGastrica || '';
          
          if (patient.usoProtecaoGastrica === 'Sim' && elements.protecaoGastricaDetails) {
            elements.protecaoGastricaDetails.classList.remove('hidden');
            
            if (elements.tipoProtecaoGastrica) {
              elements.tipoProtecaoGastrica.value = patient.tipoProtecaoGastrica || '';
            }
          }
        }
        
        // Preencher trombofilaxia
        if (elements.usoTrombofilaxia) {
          elements.usoTrombofilaxia.value = patient.usoTrombofilaxia || '';
          
          if (patient.usoTrombofilaxia === 'Sim' && elements.trombofilaxiaDetails) {
            elements.trombofilaxiaDetails.classList.remove('hidden');
            
            if (elements.tipoTrombofilaxia) {
              elements.tipoTrombofilaxia.value = patient.tipoTrombofilaxia || '';
            }
          }
        }
        
        // Preencher controle glicêmico
        if (elements.glicemiaAtual) {
          elements.glicemiaAtual.value = patient.glicemiaAtual || '';
        }
        
        if (elements.controleGlicemico) {
          elements.controleGlicemico.value = patient.controleGlicemico || '';
        }
        
        // Preencher cabeceira e conforto
        if (elements.elevacaoCabeceira) {
          elements.elevacaoCabeceira.value = patient.elevacaoCabeceira || '';
        }
        
        if (elements.nivelConforto) {
          elements.nivelConforto.value = patient.nivelConforto || '';
        }
        
        // Preencher pendências/condutas
        if (elements.pendenciasCondutas) {
          elements.pendenciasCondutas.value = patient.pendenciasCondutas || '';
        }
        
        // Preencher cateteres
        if (patient.tipoCateter && Array.isArray(patient.tipoCateter)) {
          elements.cateteresContainer.innerHTML = '';
          
          for (let i = 0; i < patient.tipoCateter.length; i++) {
            const cateterEntry = createCateterEntry();
            
            // Preencher dados do cateter
            const tipoCateter = cateterEntry.querySelector('.tipo-cateter');
            if (tipoCateter) {
              tipoCateter.value = patient.tipoCateter[i] || '';
            }
            
            const localizacaoCateter = cateterEntry.querySelector('.localizacao-cateter');
            if (localizacaoCateter && patient.localizacaoCateter && patient.localizacaoCateter[i]) {
              localizacaoCateter.value = patient.localizacaoCateter[i];
            }
            
            const dataInsercaoCateter = cateterEntry.querySelector('.data-insercao-cateter');
            if (dataInsercaoCateter && patient.dataInsercaoCateter && patient.dataInsercaoCateter[i]) {
              dataInsercaoCateter.value = formatInputDate(patient.dataInsercaoCateter[i]);
            }
            
            const tempoUsoCateter = cateterEntry.querySelector('.tempo-uso-cateter');
            if (tempoUsoCateter && patient.tempoUsoCateter && patient.tempoUsoCateter[i]) {
              tempoUsoCateter.value = patient.tempoUsoCateter[i];
            }
            
            elements.cateteresContainer.appendChild(cateterEntry);
          }
        }
        
        // Preencher sondas
        if (patient.tipoSonda && Array.isArray(patient.tipoSonda)) {
          elements.sondasContainer.innerHTML = '';
          
          for (let i = 0; i < patient.tipoSonda.length; i++) {
            const sondaEntry = createSondaEntry();
            
            // Preencher dados da sonda
            const tipoSonda = sondaEntry.querySelector('select[name="tipoSonda[]"]');
            if (tipoSonda) {
              tipoSonda.value = patient.tipoSonda[i] || '';
            }
            
            const valorDrenado = sondaEntry.querySelector('input[name="valorDrenado[]"]');
            if (valorDrenado && patient.valorDrenado && patient.valorDrenado[i]) {
              valorDrenado.value = patient.valorDrenado[i];
            }
            
            elements.sondasContainer.appendChild(sondaEntry);
          }
        }
        
        // Preencher drogas vasoativas
        if (patient.drogaVasoativa && Array.isArray(patient.drogaVasoativa)) {
          elements.drogasContainer.innerHTML = '';
          
          for (let i = 0; i < patient.drogaVasoativa.length; i++) {
            const drogaEntry = createDrogaEntry();
            
            // Preencher dados da droga
            const drogaVasoativa = drogaEntry.querySelector('select[name="drogaVasoativa[]"]');
            if (drogaVasoativa) {
              drogaVasoativa.value = patient.drogaVasoativa[i] || '';
            }
            
            const vazaoDroga = drogaEntry.querySelector('input[name="vazaoDroga[]"]');
            if (vazaoDroga && patient.vazaoDroga && patient.vazaoDroga[i]) {
              vazaoDroga.value = patient.vazaoDroga[i];
            }
            
            // Atualizar a concentração calculada
            const concentracaoDroga = drogaEntry.querySelector('.concentracao-calculada');
            if (concentracaoDroga && patient.concentracaoDroga && patient.concentracaoDroga[i]) {
              concentracaoDroga.value = patient.concentracaoDroga[i];
            } else if (concentracaoDroga && drogaVasoativa.value && vazaoDroga.value && elements.peso.value) {
              calcularConcentracaoDroga(drogaEntry);
            }
            
            elements.drogasContainer.appendChild(drogaEntry);
          }
        }
        
        // Preencher sedação
        if (patient.medicacaosedacao && Array.isArray(patient.medicacaosedacao)) {
          elements.sedacaoContainer.innerHTML = '';
          
          for (let i = 0; i < patient.medicacaosedacao.length; i++) {
            const sedacaoEntry = createMedicationEntry('sedacao');
            
            // Preencher dados da sedação
            const medicacaoSedacao = sedacaoEntry.querySelector('select[name="medicacaosedacao[]"]');
            if (medicacaoSedacao) {
              medicacaoSedacao.value = patient.medicacaosedacao[i] || '';
            }
            
            const doseSedacao = sedacaoEntry.querySelector('input[name="dosesedacao[]"]');
            if (doseSedacao && patient.dosesedacao && patient.dosesedacao[i]) {
              doseSedacao.value = patient.dosesedacao[i];
            }
            
            elements.sedacaoContainer.appendChild(sedacaoEntry);
          }
        }
        
        // Preencher analgesia
        if (patient.medicacaoanalgesia && Array.isArray(patient.medicacaoanalgesia)) {
          elements.analgesiaContainer.innerHTML = '';
          
          for (let i = 0; i < patient.medicacaoanalgesia.length; i++) {
            const analgesiaEntry = createMedicationEntry('analgesia');
            
            // Preencher dados da analgesia
            const medicacaoAnalgesia = analgesiaEntry.querySelector('select[name="medicacaoanalgesia[]"]');
            if (medicacaoAnalgesia) {
              medicacaoAnalgesia.value = patient.medicacaoanalgesia[i] || '';
            }
            
            const doseAnalgesia = analgesiaEntry.querySelector('input[name="doseanalgesia[]"]');
            if (doseAnalgesia && patient.doseanalgesia && patient.doseanalgesia[i]) {
              doseAnalgesia.value = patient.doseanalgesia[i];
            }
            
            elements.analgesiaContainer.appendChild(analgesiaEntry);
          }
        }
        
        // Preencher antibióticos
        if (patient.antibiotico && Array.isArray(patient.antibiotico)) {
          elements.antibioticosContainer.innerHTML = '';
          
          for (let i = 0; i < patient.antibiotico.length; i++) {
            const antibioticoEntry = createAntibioticoEntry();
            
            // Preencher dados do antibiótico
            const antibiotico = antibioticoEntry.querySelector('select[name="antibiotico[]"]');
            if (antibiotico) {
              antibiotico.value = patient.antibiotico[i] || '';
              
              // Verificar se é "Outro" para mostrar campo adicional
              if (patient.antibiotico[i] === 'Outro') {
                const outroAntibioticoContainer = antibioticoEntry.querySelector('.outro-antibiotico');
                if (outroAntibioticoContainer) {
                  outroAntibioticoContainer.classList.remove('hidden');
                }
                
                const outroAntibiotico = antibioticoEntry.querySelector('input[name="outroAntibiotico[]"]');
                if (outroAntibiotico && patient.outroAntibiotico && patient.outroAntibiotico[i]) {
                  outroAntibiotico.value = patient.outroAntibiotico[i];
                }
              }
            }
            
            const dataInicioAntibiotico = antibioticoEntry.querySelector('input[name="dataInicioAntibiotico[]"]');
            if (dataInicioAntibiotico && patient.dataInicioAntibiotico && patient.dataInicioAntibiotico[i]) {
              dataInicioAntibiotico.value = formatInputDate(patient.dataInicioAntibiotico[i]);
            }
            
            const tempoUsoAntibiotico = antibioticoEntry.querySelector('input[name="tempoUsoAntibiotico[]"]');
            if (tempoUsoAntibiotico && patient.tempoUsoAntibiotico && patient.tempoUsoAntibiotico[i]) {
              tempoUsoAntibiotico.value = patient.tempoUsoAntibiotico[i];
            }
            
            elements.antibioticosContainer.appendChild(antibioticoEntry);
          }
        }
      }
      
      // Formatar data para input date (YYYY-MM-DD)
      function formatInputDate(dateString) {
        if (!dateString) return '';
        
        try {
          const date = new Date(dateString);
          return date.toISOString().split('T')[0];
        } catch (e) {
          console.error('Erro ao formatar data:', e);
          return '';
        }
      }
      
      // Formatar data e hora para input datetime-local (YYYY-MM-DDThh:mm)
      function formatInputDateTime(dateString) {
        if (!dateString) return '';
        
        try {
          const date = new Date(dateString);
          return date.toISOString().slice(0, 16);
        } catch (e) {
          console.error('Erro ao formatar data e hora:', e);
          return '';
        }
      }
      
      // Formatar data para exibição
      function formatDate(date, includeTime = false) {
        if (!date) return 'N/A';
        
        try {
          const options = { 
            day: '2-digit', 
            month: '2-digit', 
            year: 'numeric' 
          };
          
          if (includeTime) {
            options.hour = '2-digit';
            options.minute = '2-digit';
          }
          
          return date.toLocaleDateString('pt-BR', options);
        } catch (e) {
          console.error('Erro ao formatar data para exibição:', e);
          return 'Data inválida';
        }
      }

      // Função para resetar o formulário
      function resetForm() {
        document.getElementById('roundMatinalForm').reset();
        
        // Limpar containers dinâmicos
        elements.cateteresContainer.innerHTML = '';
        elements.sondasContainer.innerHTML = '';
        elements.drogasContainer.innerHTML = '';
        elements.sedacaoContainer.innerHTML = '';
        elements.analgesiaContainer.innerHTML = '';
        elements.antibioticosContainer.innerHTML = '';
        
        // Adicionar uma entrada em cada container
        elements.cateteresContainer.appendChild(createCateterEntry());
        elements.sondasContainer.appendChild(createSondaEntry());
        elements.drogasContainer.appendChild(createDrogaEntry());
        elements.sedacaoContainer.appendChild(createMedicationEntry('sedacao'));
        elements.analgesiaContainer.appendChild(createMedicationEntry('analgesia'));
        elements.antibioticosContainer.appendChild(createAntibioticoEntry());
        
        // Esconder seções condicionais
        elements.intubacaoDetails.classList.add('hidden');
        elements.ventilacaoParametros.classList.add('hidden');
        elements.psvDetails.classList.add('hidden');
        elements.traqueostomiaContainer.classList.add('hidden');
        elements.dataTraqueostomiaContainer.classList.add('hidden');
        elements.quantidadeContainer.classList.add('hidden');
        elements.protecaoGastricaDetails.classList.add('hidden');
        elements.trombofilaxiaDetails.classList.add('hidden');
        
        // Resetar valores calculados
        elements.idade.value = '';
        elements.tempoInternacao.value = '';
        elements.tempoIntubacao.value = '';
        elements.tempoDesdeEvacuacao.value = '';
      }

      // Função para voltar ao menu principal
      function backToMainMenu() {
        // Verificar se há dados não salvos
        if (formState.isDirty) {
          if (!confirm('Há dados não salvos. Tem certeza que deseja sair sem salvar?')) {
            return;
          }
        }
        
        // Esconder formulário e mostrar menu principal
        formTabs.classList.add('hidden');
        roundForm.classList.add('hidden');
        mainMenu.classList.remove('hidden');
        
        // Limpar formulário
        resetForm();
      }
      
      // Adicionar botão de voltar ao menu principal
      const returnToMenuBtn = document.createElement('button');
      returnToMenuBtn.className = 'btn btn-primary fixed top-4 left-4 z-20';
      returnToMenuBtn.innerHTML = '<span>&larr;</span> Menu';
      returnToMenuBtn.addEventListener('click', backToMainMenu);
      document.body.appendChild(returnToMenuBtn);

      // Configurações iniciais
      const hoje = new Date();
      if (elements.dataPreenchimento) {
        elements.dataPreenchimento.valueAsDate = hoje;
      }
      
      // Função para mostrar toast de notificação
      function showToast(message, duration = 3000) {
        const toast = document.getElementById('toast');
        toast.textContent = message;
        toast.classList.add('show');
        
        setTimeout(() => {
          toast.classList.remove('show');
        }, duration);
      }

      // Funções de cálculo
      function calculateDays(startDate, endDate) {
        const start = new Date(startDate);
        const end = new Date(endDate);
        const diffTime = Math.abs(end - start);
        return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
      }

      // Função para calcular idade a partir da data de nascimento
      function calcularIdade() {
        if (!elements.dataNascimento.value) {
          elements.idade.value = '';
          return;
        }
        
        const dataNascimento = new Date(elements.dataNascimento.value);
        const hoje = new Date();
        
        if (dataNascimento > hoje) {
          showToast('A data de nascimento não pode ser no futuro', 5000);
          elements.dataNascimento.value = '';
          elements.idade.value = '';
          return;
        }
        
        let idade = hoje.getFullYear() - dataNascimento.getFullYear();
        const m = hoje.getMonth() - dataNascimento.getMonth();
        
        if (m < 0 || (m === 0 && hoje.getDate() < dataNascimento.getDate())) {
          idade--;
        }
        
        elements.idade.value = idade + ' anos';
        
        formState.isDirty = true;
      }

      // Função para atualizar todas as datas máximas
      function atualizarDataMaxima() {
        const agora = new Date();
        const dataFormatada = agora.toISOString().slice(0, 16);
        
        if (elements.dataIntubacao) {
          elements.dataIntubacao.max = dataFormatada;
        }
        
        if (elements.dataTraqueostomia) {
          elements.dataTraqueostomia.max = dataFormatada;
        }
        
        if (elements.dataUltimaEvacuacao) {
          elements.dataUltimaEvacuacao.max = dataFormatada;
        }
      }

      // Funções de Ventilação Mecânica
      function limparCamposIntubacao() {
        elements.tempoIntubacao.value = '';
        elements.statusIntubacao.className = 'status-indicator';
        elements.traqueostomiaContainer.classList.add('hidden');
        if (elements.realizouTraqueostomia) {
          elements.realizouTraqueostomia.checked = false;
        }
        if (elements.dataTraqueostomia) {
          elements.dataTraqueostomia.value = '';
        }
      }

      function calcularTempoIntubacao() {
        if (!elements.dataIntubacao || !elements.dataIntubacao.value) {
          limparCamposIntubacao();
          return;
        }
        
        const dataInicio = new Date(elements.dataIntubacao.value);
        const agora = new Date();
        
        if (isNaN(dataInicio.getTime())) {
          limparCamposIntubacao();
          return;
        }

        if (dataInicio > agora) {
          showToast('A data de intubação não pode ser no futuro', 5000);
          elements.dataIntubacao.value = '';
          limparCamposIntubacao();
          return;
        }

        const diffMs = agora - dataInicio;
        const diffDias = Math.floor(diffMs / (1000 * 60 * 60 * 24));
        const diffHoras = Math.floor((diffMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));

        elements.tempoIntubacao.value = `${diffDias} dia(s) e ${diffHoras} hora(s)`;

        // Atualizar status visual
        elements.tempoIntubacao.style.color = '';
        elements.statusIntubacao.className = 'status-indicator';

        if (diffDias >= 11) {
          elements.tempoIntubacao.style.color = 'var(--danger-color)';
          elements.statusIntubacao.classList.add('status-danger');
        } else if (diffDias >= 6) {
          elements.tempoIntubacao.style.color = 'var(--warning-color)';
          elements.statusIntubacao.classList.add('status-warning');
        } else {
          elements.statusIntubacao.classList.add('status-ok');
        }

        // Verificar necessidade de traqueostomia
        if (diffDias > 5) {
          elements.traqueostomiaContainer.classList.remove('hidden');
        } else {
          elements.traqueostomiaContainer.classList.add('hidden');
          if (elements.realizouTraqueostomia) {
            elements.realizouTraqueostomia.checked = false;
          }
          if (elements.dataTraqueostomia) {
            elements.dataTraqueostomia.value = '';
          }
        }
        
        formState.isDirty = true;
      }
      
      // Função para cálculo do tempo desde última evacuação
      function calcularTempoDesdeEvacuacao() {
        if (!elements.dataUltimaEvacuacao || !elements.dataUltimaEvacuacao.value) {
          elements.tempoDesdeEvacuacao.value = '';
          return;
        }
        
        const dataEvacuacao = new Date(elements.dataUltimaEvacuacao.value);
        const agora = new Date();
        
        if (isNaN(dataEvacuacao.getTime())) {
          elements.tempoDesdeEvacuacao.value = '';
          return;
        }

        if (dataEvacuacao > agora) {
          showToast('A data da última evacuação não pode ser no futuro', 5000);
          elements.dataUltimaEvacuacao.value = '';
          return;
        }

        const diffMs = agora - dataEvacuacao;
        const diffHoras = Math.floor(diffMs / (1000 * 60 * 60));
        const diffDias = Math.floor(diffHoras / 24);
        const horasRestantes = diffHoras % 24;

        elements.tempoDesdeEvacuacao.value = `${diffDias} dia(s) e ${horasRestantes} hora(s)`;

        // Atualizar estilo baseado no tempo
        if (diffHoras >= 72) {
          elements.tempoDesdeEvacuacao.style.color = 'var(--danger-color)';
          elements.tempoDesdeEvacuacao.style.fontWeight = 'bold';
        } else if (diffHoras >= 48) {
          elements.tempoDesdeEvacuacao.style.color = 'var(--warning-color)';
          elements.tempoDesdeEvacuacao.style.fontWeight = 'bold';
        } else {
          elements.tempoDesdeEvacuacao.style.color = 'var(--success-color)';
          elements.tempoDesdeEvacuacao.style.fontWeight = 'normal';
        }
        
        formState.isDirty = true;
      }

      // Função para validação do formulário
      function validateForm() {
        let isValid = true;
        const requiredFields = document.querySelectorAll('[required]');
        
        requiredFields.forEach(field => {
          if (!field.value) {
            field.classList.add('invalid');
            isValid = false;
            
            if (!field.nextElementSibling?.classList.contains('validation-message')) {
              const message = document.createElement('div');
              message.className = 'validation-message';
              message.textContent = 'Este campo é obrigatório';
              field.parentNode.insertBefore(message, field.nextSibling);
            }
          } else {
            field.classList.remove('invalid');
            const message = field.nextElementSibling;
            if (message?.classList.contains('validation-message')) {
              message.remove();
            }
          }
        });

        return isValid;
      }

      // Função para calcular a concentração de droga vasoativa (μcg/kg/min)
      function calcularConcentracaoDroga(drogaEntry) {
        const pesoInput = elements.peso;
        const drogaSelect = drogaEntry.querySelector('select[name="drogaVasoativa[]"]');
        const vazaoInput = drogaEntry.querySelector('input[name="vazaoDroga[]"]');
        const concentracaoOutput = drogaEntry.querySelector('.concentracao-calculada');
        
        if (!pesoInput || !pesoInput.value || !drogaSelect || !drogaSelect.value || !vazaoInput || !vazaoInput.value || !concentracaoOutput) {
          return;
        }
        
        const peso = parseFloat(pesoInput.value);
        const vazao = parseFloat(vazaoInput.value);
        
        if (isNaN(peso) || isNaN(vazao) || peso <= 0 || vazao < 0) {
          concentracaoOutput.value = '';
          return;
        }
        
        // Concentrações padrão das drogas em mg/ml
        const concentracaoPadrao = {
          'Noradrenalina': 16/250, // 16mg em 250ml (0.064 mg/ml)
          'Dobutamina': 250/250,   // 250mg em 250ml (1 mg/ml)
          'Adrenalina': 5/250,     // 5mg em 250ml (0.02 mg/ml)
          'Vasopressina': 20/100,  // 20U em 100ml (0.2 U/ml)
          'Nitroprussiato': 50/250, // 50mg em 250ml (0.2 mg/ml)
          'Nitroglicerina': 50/250, // 50mg em 250ml (0.2 mg/ml)
          'Amiodarona': 150/250,    // 150mg em 250ml (0.6 mg/ml)
        };
        
        let concentracao = 0;
        const droga = drogaSelect.value;
        
        if (droga !== 'Nenhuma') {
          // Fórmula: (vazão (ml/h) × concentração (mg/ml) × 1000) / (peso (kg) × 60)
          // Convertendo mg para μcg (×1000) e hora para minuto (÷60)
          if (droga === 'Vasopressina') {
            // Para Vasopressina, a unidade é U/kg/h
            concentracao = (vazao * concentracaoPadrao[droga]) / peso;
            concentracaoOutput.value = concentracao.toFixed(3) + ' U/kg/h';
          } else if (concentracaoPadrao[droga]) {
            concentracao = (vazao * concentracaoPadrao[droga] * 1000) / (peso * 60);
            concentracaoOutput.value = concentracao.toFixed(2) + ' μcg/kg/min';
          } else {
            concentracaoOutput.value = 'N/A';
          }
        } else {
          concentracaoOutput.value = '';
        }
        
        formState.isDirty = true;
      }

      // Funções para criar elementos dinâmicos
      function createCateterEntry() {
        const entry = document.createElement('div');
        entry.classList.add('medication-entry');
        entry.innerHTML = `
          <div class="flex-container">
            <div class="form-group">
              <label for="tipoCateter" class="form-label">Tipo de Cateter:</label>
              <select name="tipoCateter[]" class="form-control tipo-cateter" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="Cateter Central">Cateter Central</option>
                <option value="Cateter Periférico">Cateter Periférico</option>
                <option value="Cateter de Diálise">Cateter de Diálise</option>
                <option value="Outro">Outro</option>
              </select>
            </div>
            <div class="form-group">
              <label for="localizacaoCateter" class="form-label">Localização:</label>
              <select name="localizacaoCateter[]" class="form-control localizacao-cateter">
                <option value="" disabled selected>Selecione a localização</option>
                <option value="VJD">VJD</option>
                <option value="VJE">VJE</option>
                <option value="VSCD">VSCD</option>
                <option value="VSCE">VSCE</option>
                <option value="FD">FD</option>
                <option value="FE">FE</option>
                <option value="MSD">MSD</option>
                <option value="MSE">MSE</option>
                <option value="MID">MID</option>
                <option value="MIE">MIE</option>
                <option value="Outros">Outros</option>
              </select>
            </div>
          </div>
          <div class="flex-container">
            <div class="form-group">
              <label for="dataInsercaoCateter" class="form-label">Data de Inserção:</label>
              <input type="date" name="dataInsercaoCateter[]" class="form-control data-insercao-cateter">
            </div>
            <div class="form-group">
              <label for="tempoUsoCateter" class="form-label">Tempo de Uso:</label>
              <input type="text" name="tempoUsoCateter[]" class="form-control tempo-uso-cateter" readonly placeholder="Será calculado automaticamente">
            </div>
          </div>
          <button type="button" class="btn btn-danger remove-btn">Remover</button>
        `;

        const dataInsercaoInput = entry.querySelector('.data-insercao-cateter');
        const tempoUsoInput = entry.querySelector('.tempo-uso-cateter');
        
        // Marcar formulário como modificado quando o valor for alterado
        entry.querySelectorAll('input, select').forEach(input => {
          input.addEventListener('change', () => {
            formState.isDirty = true;
          });
        });
        
        // Adicionar evento para calcular tempo de uso quando a data mudar
        dataInsercaoInput.addEventListener('change', () => {
          calcularTempoUso(dataInsercaoInput, tempoUsoInput);
        });
        
        // Adicionar evento para remover a entrada quando o botão de remover for clicado
        entry.querySelector('.remove-btn').addEventListener('click', () => {
          entry.remove();
          formState.isDirty = true;
        });
        
        return entry;
      }

      function createSondaEntry() {
        const entry = document.createElement('div');
        entry.classList.add('medication-entry');
        entry.innerHTML = `
          <div class="flex-container">
            <div class="form-group">
              <label for="tipoSonda" class="form-label">Tipo de Sonda:</label>
              <select name="tipoSonda[]" class="form-control" required>
                <option value="" disabled selected>Selecione uma opção</option>
                <option value="SVD">SVD</option>
                <option value="SR">SR</option>
                <option value="Dreno de Tórax">Dreno de Tórax</option>
                <option value="Drenos Abdominais">Drenos Abdominais</option>
                <option value="Outros Drenos">Outros Drenos</option>
              </select>
            </div>
            <div class="form-group">
              <label for="valorDrenado" class="form-label">Valor Drenado (ml):</label>
              <input type="number" name="valorDrenado[]" class="form-control" placeholder="Insira o valor drenado">
            </div>
          </div>
          <button type="button" class="btn btn-danger remove-btn">Remover</button>
        `;
        
        // Marcar formulário como modificado quando o valor for alterado
        entry.querySelectorAll('input, select').forEach(input => {
          input.addEventListener('change', () => {
            formState.isDirty = true;
          });
        });
        
        // Adicionar evento para remover a entrada quando o botão de remover for clicado
        entry.querySelector('.remove-btn').addEventListener('click', () => {
          entry.remove();
          formState.isDirty = true;
        });
        
        return entry;
      }

      function createDrogaEntry() {
        const entry = document.createElement('div');
        entry.classList.add('medication-entry');
        entry.innerHTML = `
          <div class="flex-container">
            <div class="form-group">
              <label for="drogaVasoativa" class="form-label">Droga Vasoativa:</label>
              <select name="drogaVasoativa[]" class="form-control droga-vasoativa-select" required>
                <option value="" disabled selected>Selecione uma droga</option>
                <option value="Noradrenalina">Noradrenalina</option>
                <option value="Vasopressina">Vasopressina</option>
                <option value="Dobutamina">Dobutamina</option>
                <option value="Adrenalina">Adrenalina</option>
                <option value="Nitroprussiato">Nitroprussiato</option>
                <option value="Nitroglicerina">Nitroglicerina</option>
                <option value="Amiodarona">Amiodarona</option>
                <option value="Nenhuma">Nenhuma</option>
              </select>
            </div>
            <div class="form-group">
              <label for="vazaoDroga" class="form-label">Vazão (ml/h):</label>
              <input type="number" name="vazaoDroga[]" class="form-control vazao-droga-input" placeholder="Informe a vazão">
            </div>
          </div>
          
          <div class="form-group">
            <label class="form-label">Concentração calculada:</label>
            <input type="text" class="form-control concentracao-calculada" name="concentracaoDroga[]" readonly placeholder="Será calculada automaticamente com base no peso">
          </div>
          
          <button type="button" class="btn btn-danger remove-btn">Remover</button>
        `;
        
        const drogaSelect = entry.querySelector('.droga-vasoativa-select');
        const vazaoInput = entry.querySelector('.vazao-droga-input');
        
        // Marcar formulário como modificado e calcular concentração quando valores forem alterados
        drogaSelect.addEventListener('change', () => {
          formState.isDirty = true;
          calcularConcentracaoDroga(entry);
        });
        
        vazaoInput.addEventListener('change', () => {
          formState.isDirty = true;
          calcularConcentracaoDroga(entry);
        });
        
        // Adicionar evento para recalcular quando o peso mudar
        if (elements.peso) {
          elements.peso.addEventListener('change', () => {
            // Recalcular todas as concentrações de drogas
            document.querySelectorAll('.medication-entry').forEach(drogaEntry => {
              if (drogaEntry.querySelector('.concentracao-calculada')) {
                calcularConcentracaoDroga(drogaEntry);
              }
            });
          });
        }
        
        // Adicionar evento para remover a entrada quando o botão de remover for clicado
        entry.querySelector('.remove-btn').addEventListener('click', () => {
          entry.remove();
          formState.isDirty = true;
        });
        
        return entry;
      }

      function createMedicationEntry(type) {
        const entry = document.createElement('div');
        entry.classList.add('medication-entry');
        
        const selectOptions = type === 'sedacao' 
          ? `<option value="Midazolan">Midazolan</option>
              <option value="Propofol">Propofol</option>
              <option value="Cetamina">Cetamina</option>
              <option value="Dexmedetomidina">Dexmedetomidina</option>`
          : `<option value="Dipirona">Dipirona</option>
              <option value="Morfina">Morfina</option>
              <option value="Fentanil">Fentanil</option>
              <option value="Metadona">Metadona</option>`;

        entry.innerHTML = `
          <div class="flex-container">
            <div class="form-group">
              <label for="medicacao${type}" class="form-label">Medicação:</label>
              <select class="form-control medicacao-dropdown" name="medicacao${type}[]" required>
                <option value="" disabled selected>Selecione uma opção</option>
                ${selectOptions}
                <option value="Outros">Outros</option>
              </select>
            </div>
            <div class="form-group">
              <label for="dose${type}" class="form-label">Dose em uso (${type === 'sedacao' ? 'mg/h' : 'mg'}):</label>
              <input type="text" class="form-control dose-input" name="dose${type}[]" placeholder="Informe a dose">
            </div>
          </div>
          <button type="button" class="btn btn-danger remove-btn">Remover</button>
        `;

        // Marcar formulário como modificado quando o valor for alterado
        entry.querySelectorAll('input, select').forEach(input => {
          input.addEventListener('change', () => {
            formState.isDirty = true;
          });
        });

        entry.querySelector('.remove-btn').addEventListener('click', () => {
          entry.remove();
          formState.isDirty = true;
        });
        
        return entry;
      }

      function createAntibioticoEntry() {
        const entry = document.createElement('div');
        entry.classList.add('medication-entry');
        entry.innerHTML = `
          <div class="form-group">
            <label for="antibiotico" class="form-label">Antibiótico:</label>
            <select class="form-control antibiotico-dropdown" name="antibiotico[]" required>
              <option value="" disabled selected>Selecione um antibiótico</option>
              <option value="Vancomicina">Vancomicina</option>
              <option value="Ceftriaxone">Ceftriaxone</option>
              <option value="Meropenem">Meropenem</option>
              <option value="Tazo-Pipe">Tazo</option>
              <option value="Poli B">Poli B</option>
              <option value="Metronidazol">Metro</option>
              <option value="Fluconazol">Fluco</option>
              <option value="Cefalotina">Cefalo</option>
              <option value="Claritromicina">Claritromicina</option>
              <option value="Clindamicina">Clindamicina</option>
              <option value="Amicacina">Amicacina</option>
              <option value="Azitromicina">Azitromicina</option>
              <option value="Outro">Outro</option>
            </select>
          </div>
          
          <div class="outro-antibiotico hidden">
            <div class="form-group">
              <label for="outroAntibiotico" class="form-label">Nome do Antibiótico:</label>
              <input type="text" class="form-control" name="outroAntibiotico[]" placeholder="Digite o nome do antibiótico">
            </div>
          </div>

          <div class="flex-container">
            <div class="form-group">
              <label for="dataInicioAntibiotico" class="form-label">Data de Início:</label>
              <input type="date" class="form-control data-inicio-antibiotico" name="dataInicioAntibiotico[]" required>
            </div>
            <div class="form-group">
              <label for="tempoUsoAntibiotico" class="form-label">Tempo de Uso (dias):</label>
              <input type="text" class="form-control tempo-uso-antibiotico" name="tempoUsoAntibiotico[]" readonly placeholder="Calculado automaticamente">
            </div>
          </div>

          <button type="button" class="btn btn-danger remove-btn">Remover</button>
        `;

        const antibioticoDropdown = entry.querySelector('.antibiotico-dropdown');
        const outroAntibioticoContainer = entry.querySelector('.outro-antibiotico');
        
        // Marcar formulário como modificado quando o valor for alterado
        entry.querySelectorAll('input, select').forEach(input => {
          input.addEventListener('change', () => {
            formState.isDirty = true;
          });
        });
        
        antibioticoDropdown.addEventListener('change', function() {
          outroAntibioticoContainer.classList.toggle('hidden', this.value !== 'Outro');
        });

        entry.querySelector('.remove-btn').addEventListener('click', () => {
          entry.remove();
          formState.isDirty = true;
        });
        
        const dataInicioInput = entry.querySelector('.data-inicio-antibiotico');
        const tempoUsoInput = entry.querySelector('.tempo-uso-antibiotico');
        
        dataInicioInput.addEventListener('change', () => {
          calcularTempoUsoAntibiotico(dataInicioInput, tempoUsoInput);
        });

        return entry;
      }

      // Função para cálculo do tempo de uso
      function calcularTempoUso(dataInsercaoInput, tempoUsoInput) {
        const dataInsercao = new Date(dataInsercaoInput.value);
        const hoje = new Date();
        
        if (!dataInsercaoInput.value) {
          tempoUsoInput.value = '';
          return;
        }
        
        if (dataInsercao > hoje) {
          showToast('A data de inserção não pode ser no futuro', 5000);
          dataInsercaoInput.value = '';
          tempoUsoInput.value = '';
          return;
        }

        const diffMs = hoje - dataInsercao;
        const diffDias = Math.floor(diffMs / (1000 * 60 * 60 * 24));
        tempoUsoInput.value = `${diffDias} dia(s)`;
        
        // Aplicar destaque para cateter com uso prolongado
        if (diffDias > 7) {
          tempoUsoInput.style.color = 'var(--warning-color)';
          tempoUsoInput.style.fontWeight = 'bold';
        } else {
          tempoUsoInput.style.color = '';
          tempoUsoInput.style.fontWeight = 'normal';
        }
        
        formState.isDirty = true;
      }

      // Função para cálculo do tempo de uso de antibióticos
      function calcularTempoUsoAntibiotico(dataInicioInput, tempoUsoInput) {
        const dataInicio = new Date(dataInicioInput.value);
        const hoje = new Date();
        
        if (!dataInicioInput.value) {
          tempoUsoInput.value = '';
          return;
        }
        
        if (dataInicio > hoje) {
          showToast('A data de início não pode ser no futuro', 5000);
          dataInicioInput.value = '';
          tempoUsoInput.value = '';
          return;
        }

        const diffMs = hoje - dataInicio;
        const diffDias = Math.floor(diffMs / (1000 * 60 * 60 * 24));
        tempoUsoInput.value = `${diffDias} dia(s)`;
        
        // Aplicar destaque para antibióticos com uso prolongado
        if (diffDias > 10) {
          tempoUsoInput.style.color = 'var(--danger-color)';
          tempoUsoInput.style.fontWeight = 'bold';
        } else if (diffDias > 7) {
          tempoUsoInput.style.color = 'var(--warning-color)';
          tempoUsoInput.style.fontWeight = 'bold';
        } else {
          tempoUsoInput.style.color = '';
          tempoUsoInput.style.fontWeight = 'normal';
        }
        
        formState.isDirty = true;
      }

      // Função para gerar resumo
      function generateSummary() {
        const resumoContent = document.getElementById('resumoContent');
        const loadingResumo = document.getElementById('loadingResumo');
        
        // Mostrar loading e limpar conteúdo anterior
        loadingResumo.style.display = 'block';
        resumoContent.innerHTML = '<div id="loadingResumo" class="spinner"></div>';
        
        // Simular carregamento para experiência do usuário
        setTimeout(() => {
          const formData = new FormData(document.getElementById('roundMatinalForm'));
          const data = {};
          
          for (const [key, value] of formData.entries()) {
            if (key.endsWith('[]')) {
              const baseKey = key.slice(0, -2);
              if (!data[baseKey]) {
                data[baseKey] = [];
              }
              data[baseKey].push(value);
            } else {
              data[key] = value;
            }
          }
          
          // Criar conteúdo HTML do resumo
          let html = `
            <div class="card">
              <h3 class="text-lg font-semibold">Identificação do Paciente</h3>
              <div class="table-container">
                <table>
                  <tr>
                    <th>Nome</th>
                    <td>${data.nomePaciente || 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Registro</th>
                    <td>${data.registroHospitalar || 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Leito</th>
                    <td>${data.leito || 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Data de Nascimento</th>
                    <td>${formatarData(data.dataNascimento) || 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Idade</th>
                    <td>${data.idade || 'Não calculado'}</td>
                  </tr>
                  <tr>
                    <th>Peso</th>
                    <td>${data.peso ? `${data.peso} kg` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Internação</th>
                    <td>${formatarData(data.dataInternacao)} (${data.tempoInternacao || 'Não calculado'})</td>
                  </tr>
                </table>
              </div>
            </div>
          `;
          
          // Ventilação Mecânica
          html += `
            <div class="card mt-4">
              <h3 class="text-lg font-semibold">Status Ventilatório</h3>
              <div class="table-container">
                <table>
                  <tr>
                    <th>Intubado</th>
                    <td>${data.pacienteIntubado || 'Não informado'}</td>
                  </tr>
          `;
          
          if (data.pacienteIntubado === 'Sim') {
            html += `
                  <tr>
                    <th>Tempo de Intubação</th>
                    <td>${data.tempoIntubacao || 'Não calculado'}</td>
                  </tr>
                  <tr>
                    <th>Modo Ventilação</th>
                    <td>${data.modoVentilacao || 'Não informado'}</td>
                  </tr>
            `;
            
            if (data.modoVentilacao) {
              html += `
                  <tr>
                    <th>FiO2</th>
                    <td>${data.fio2 ? `${data.fio2}%` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>FR</th>
                    <td>${data.fr ? `${data.fr} irpm` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Pinsp</th>
                    <td>${data.pinsp ? `${data.pinsp} cmH2O` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>VC</th>
                    <td>${data.vc ? `${data.vc} ml` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Vol/m</th>
                    <td>${data.volm ? `${data.volm} ml/kg` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>PEEP</th>
                    <td>${data.peep ? `${data.peep} cmH2O` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Ppico</th>
                    <td>${data.ppico ? `${data.ppico} cmH2O` : 'Não informado'}</td>
                  </tr>
                  <tr>
                    <th>Pplato</th>
                    <td>${data.pplato ? `${data.pplato} cmH2O` : 'Não informado'}</td>
                  </tr>
              `;
            }
            
            if (data.modoVentilacao === 'PSV' && data.podeExtubar) {
              html += `
                  <tr>
                    <th>Pode Extubar</th>
                    <td>${data.podeExtubar}</td>
                  </tr>
              `;
            }
            
            if (data.realizouTraqueostomia) {
              html += `
                  <tr>
                    <th>Traqueostomia</th>
                    <td>Sim, em ${formatarData(data.dataTraqueostomia)}</td>
                  </tr>
              `;
            }
          }
          
          html += `
                </table>
              </div>
            </div>
          `;
          
          // Dispositivos
          html += `
            <div class="card mt-4">
              <h3 class="text-lg font-semibold">Dispositivos</h3>
          `;
          
          // Cateteres
          if (data.tipoCateter && data.tipoCateter.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-2">Cateteres</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Tipo</th>
                      <th>Localização</th>
                      <th>Tempo de Uso</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.tipoCateter.length; i++) {
              html += `
                    <tr>
                      <td>${data.tipoCateter[i] || 'Não informado'}</td>
                      <td>${data.localizacaoCateter && data.localizacaoCateter[i] ? data.localizacaoCateter[i] : 'Não informado'}</td>
                      <td>${data.tempoUsoCateter && data.tempoUsoCateter[i] ? data.tempoUsoCateter[i] : 'Não calculado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p>Não há cateteres registrados.</p>`;
          }
          
          // Sondas
          if (data.tipoSonda && data.tipoSonda.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-4">Sondas e Drenos</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Tipo</th>
                      <th>Valor Drenado (ml)</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.tipoSonda.length; i++) {
              html += `
                    <tr>
                      <td>${data.tipoSonda[i] || 'Não informado'}</td>
                      <td>${data.valorDrenado && data.valorDrenado[i] ? data.valorDrenado[i] : 'Não informado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p class="mt-4">Não há sondas ou drenos registrados.</p>`;
          }
          
          // Drogas Vasoativas
          if (data.drogaVasoativa && data.drogaVasoativa.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-4">Drogas Vasoativas</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Droga</th>
                      <th>Vazão (ml/h)</th>
                      <th>Concentração</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.drogaVasoativa.length; i++) {
              html += `
                    <tr>
                      <td>${data.drogaVasoativa[i] || 'Não informado'}</td>
                      <td>${data.vazaoDroga && data.vazaoDroga[i] ? data.vazaoDroga[i] : 'Não informado'}</td>
                      <td>${data.concentracaoDroga && data.concentracaoDroga[i] ? data.concentracaoDroga[i] : 'Não calculado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p class="mt-4">Não há drogas vasoativas registradas.</p>`;
          }
          
          html += `</div>`;
          
          // Medicações
          html += `
            <div class="card mt-4">
              <h3 class="text-lg font-semibold">Medicações</h3>
          `;
          
          // Sedação
          if (data.medicacaosedacao && data.medicacaosedacao.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-2">Sedação</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Medicação</th>
                      <th>Dose (mg/h)</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.medicacaosedacao.length; i++) {
              html += `
                    <tr>
                      <td>${data.medicacaosedacao[i] || 'Não informado'}</td>
                      <td>${data.dosesedacao && data.dosesedacao[i] ? data.dosesedacao[i] : 'Não informado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p>Não há medicações de sedação registradas.</p>`;
          }
          
          // Analgesia
          if (data.medicacaoanalgesia && data.medicacaoanalgesia.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-4">Analgesia</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Medicação</th>
                      <th>Dose (mg)</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.medicacaoanalgesia.length; i++) {
              html += `
                    <tr>
                      <td>${data.medicacaoanalgesia[i] || 'Não informado'}</td>
                      <td>${data.doseanalgesia && data.doseanalgesia[i] ? data.doseanalgesia[i] : 'Não informado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p class="mt-4">Não há medicações de analgesia registradas.</p>`;
          }
          
          // Antibióticos
          if (data.antibiotico && data.antibiotico.length > 0) {
            html += `
              <h4 class="text-md font-semibold mt-4">Antibióticos</h4>
              <div class="table-container">
                <table>
                  <thead>
                    <tr>
                      <th>Antibiótico</th>
                      <th>Tempo de Uso</th>
                    </tr>
                  </thead>
                  <tbody>
            `;
            
            for (let i = 0; i < data.antibiotico.length; i++) {
              let antibioticoNome = data.antibiotico[i];
              if (antibioticoNome === 'Outro' && data.outroAntibiotico && data.outroAntibiotico[i]) {
                antibioticoNome = data.outroAntibiotico[i];
              }
              
              html += `
                    <tr>
                      <td>${antibioticoNome || 'Não informado'}</td>
                      <td>${data.tempoUsoAntibiotico && data.tempoUsoAntibiotico[i] ? data.tempoUsoAntibiotico[i] : 'Não calculado'}</td>
                    </tr>
              `;
            }
            
            html += `
                  </tbody>
                </table>
              </div>
            `;
          } else {
            html += `<p class="mt-4">Não há antibióticos registrados.</p>`;
          }
          
          html += `</div>`;
          
          // Outros Parâmetros
          html += `
            <div class="card mt-4">
              <h3 class="text-lg font-semibold">Outros Parâmetros</h3>
              <div class="flex-container">
                <div>
                  <h4 class="text-md font-semibold">Alimentação</h4>
                  <p><strong>Via:</strong> ${data.viaAlimentacao || 'Não informado'}</p>
                  ${data.quantidadeDiaria ? `<p><strong>Quantidade:</strong> ${data.quantidadeDiaria} ml/dia</p>` : ''}
                </div>
                <div>
                  <h4 class="text-md font-semibold">Trânsito Intestinal</h4>
                  <p><strong>Status:</strong> ${data.transitoIntestinal || 'Não informado'}</p>
                  <p><strong>Última Evacuação:</strong> ${data.tempoDesdeEvacuacao || 'Não calculado'}</p>
                </div>
              </div>
              
              <div class="flex-container mt-4">
                <div>
                  <h4 class="text-md font-semibold">Proteção Gástrica</h4>
                  <p><strong>Em uso:</strong> ${data.usoProtecaoGastrica || 'Não informado'}</p>
                  ${data.usoProtecaoGastrica === 'Sim' ? `<p><strong>Tipo:</strong> ${data.tipoProtecaoGastrica || 'Não informado'}</p>` : ''}
                </div>
                <div>
                  <h4 class="text-md font-semibold">Trombofilaxia</h4>
                  <p><strong>Em uso:</strong> ${data.usoTrombofilaxia || 'Não informado'}</p>
                  ${data.usoTrombofilaxia === 'Sim' ? `<p><strong>Tipo:</strong> ${data.tipoTrombofilaxia || 'Não informado'}</p>` : ''}
                </div>
              </div>
              
              <div class="flex-container mt-4">
                <div>
                  <h4 class="text-md font-semibold">Controle Glicêmico</h4>
                  <p><strong>Glicemia Atual:</strong> ${data.glicemiaAtual ? `${data.glicemiaAtual} mg/dL` : 'Não informado'}</p>
                  <p><strong>Controle:</strong> ${data.controleGlicemico || 'Não informado'}</p>
                </div>
                <div>
                  <h4 class="text-md font-semibold">Cabeceira e Conforto</h4>
                  <p><strong>Elevação da Cabeceira:</strong> ${data.elevacaoCabeceira || 'Não informado'}</p>
                  <p><strong>Nível de Conforto:</strong> ${data.nivelConforto || 'Não informado'}</p>
                </div>
              </div>
              
              ${data.pendenciasCondutas ? `
              <div class="mt-4">
                <h4 class="text-md font-semibold">Pendências / Condutas</h4>
                <p>${data.pendenciasCondutas.replace(/\n/g, '<br>')}</p>
              </div>
              ` : ''}
            </div>
          `;
          
          // Atualizar o conteúdo e esconder o loading
          loadingResumo.style.display = 'none';
          resumoContent.innerHTML = html;
        }, 500);
      }

      // Função para formatar datas
      function formatarData(dataString) {
        if (!dataString) return 'Não informado';
        
        try {
          const data = new Date(dataString);
          if (isNaN(data.getTime())) return 'Data inválida';
          
          return data.toLocaleDateString('pt-BR');
        } catch (e) {
          console.error('Erro ao formatar data:', e);
          return 'Data inválida';
        }
      }

      // ============ FUNCIONALIDADES DE BANCO DE DADOS ============
      
      // Função para salvar paciente no banco de dados
      function savePatient() {
        if (!validateForm()) {
          showToast('Por favor, preencha todos os campos obrigatórios', 5000);
          return;
        }
        
        try {
          const formData = new FormData(document.getElementById('roundMatinalForm'));
          const patientData = {};
          
          for (const [key, value] of formData.entries()) {
            patientData[key] = value;
          }
          
          // Adicionar ID e timestamp
          patientData.id = currentPatientId;
          patientData.createdAt = formState.isNewPatient ? new Date().toISOString() : patientData.createdAt;
          patientData.updatedAt = new Date().toISOString();
          
          // Salvar no IndexedDB
          const transaction = db.transaction([PATIENTS_STORE], 'readwrite');
          const store = transaction.objectStore(PATIENTS_STORE);
          
          store.put(patientData);
          
          transaction.oncomplete = () => {
            formState.lastSaved = new Date();
            formState.isDirty = false;
            formState.isNewPatient = false;
            
            showToast('Paciente salvo com sucesso!', 3000);
          };
          
          transaction.onerror = (event) => {
            console.error("Erro ao salvar paciente:", event.target.error);
            showToast('Erro ao salvar paciente', 5000);
          };
        } catch (error) {
          console.error("Erro ao processar dados do paciente:", error);
          showToast('Erro ao processar dados do paciente', 5000);
        }
      }
      
      // Exportar o banco de dados para um arquivo JSON
      function exportDatabase() {
        const transaction = db.transaction([PATIENTS_STORE, SETTINGS_STORE], 'readonly');
        const patientsStore = transaction.objectStore(PATIENTS_STORE);
        const settingsStore = transaction.objectStore(SETTINGS_STORE);
        
        const patientsRequest = patientsStore.getAll();
        const settingsRequest = settingsStore.getAll();
        
        transaction.oncomplete = () => {
          const patients = patientsRequest.result || [];
          const settings = settingsRequest.result || [];
          
          const databaseDump = {
            version: DB_VERSION,
            exported_at: new Date().toISOString(),
            patients,
            settings
          };
          
          // Criar arquivo para download
          const blob = new Blob([JSON.stringify(databaseDump, null, 2)], { type: 'application/json' });
          const url = URL.createObjectURL(blob);
          const link = document.createElement('a');
          link.href = url;
          link.download = `round_matinal_uti_backup_${new Date().toISOString().split('T')[0]}.json`;
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
          
          // Atualizar a data do último backup
          updateLastBackup();
          
          showToast('Backup exportado com sucesso!', 3000);
        };
        
        transaction.onerror = (event) => {
          console.error("Erro ao exportar banco de dados:", event.target.error);
          showToast('Erro ao exportar banco de dados', 5000);
        };
      }
      
      // Mostrar modal de importação de banco de dados
      function showImportModal() {
        document.getElementById('importModal').classList.remove('hidden');
        fileInput.value = '';
        document.getElementById('confirmImport').setAttribute('disabled', 'disabled');
        dropzone.textContent = 'Arraste o arquivo de backup aqui ou clique para selecionar';
      }
      
      // Importar banco de dados a partir de um arquivo JSON
      function importDatabase() {
        const file = fileInput.files[0];
        
        if (!file) {
          showToast('Selecione um arquivo de backup', 3000);
          return;
        }
        
        const reader = new FileReader();
        
        reader.onload = (event) => {
          try {
            const data = JSON.parse(event.target.result);
            
            // Validar estrutura mínima do arquivo
            if (!data.patients || !Array.isArray(data.patients)) {
              throw new Error('Formato de arquivo inválido');
            }
            
            // Importar dados para o banco
            const transaction = db.transaction([PATIENTS_STORE, SETTINGS_STORE], 'readwrite');
            const patientsStore = transaction.objectStore(PATIENTS_STORE);
            const settingsStore = transaction.objectStore(SETTINGS_STORE);
            
            // Limpar dados existentes
            patientsStore.clear();
            
            // Adicionar pacientes
            data.patients.forEach(patient => {
              patientsStore.add(patient);
            });
            
            // Importar configurações se existirem
            if (data.settings && Array.isArray(data.settings)) {
              settingsStore.clear();
              
              data.settings.forEach(setting => {
                settingsStore.add(setting);
              });
            }
            
            transaction.oncomplete = () => {
              // Fechar modal
              document.getElementById('importModal').classList.add('hidden');
              
              // Atualizar a data do último backup
              updateLastBackup();
              
              showToast('Banco de dados importado com sucesso!', 3000);
            };
            
            transaction.onerror = (event) => {
              console.error("Erro ao importar banco de dados:", event.target.error);
              showToast('Erro ao importar banco de dados', 5000);
            };
          } catch (error) {
            console.error("Erro ao processar arquivo de importação:", error);
            showToast('Erro ao processar arquivo de importação. Verifique se o formato é válido.', 5000);
          }
        };
        
        reader.onerror = () => {
          showToast('Erro ao ler o arquivo', 3000);
        };
        
        reader.readAsText(file);
      }

      // Inicializar containers com uma entrada cada
      elements.cateteresContainer.appendChild(createCateterEntry());
      elements.sondasContainer.appendChild(createSondaEntry());
      elements.drogasContainer.appendChild(createDrogaEntry());
      elements.sedacaoContainer.appendChild(createMedicationEntry('sedacao'));
      elements.analgesiaContainer.appendChild(createMedicationEntry('analgesia'));
      elements.antibioticosContainer.appendChild(createAntibioticoEntry());

      // Event Listeners para adicionar elementos dinâmicos
      document.getElementById('addCateter').addEventListener('click', () => elements.cateteresContainer.appendChild(createCateterEntry()));
      document.getElementById('addSonda').addEventListener('click', () => elements.sondasContainer.appendChild(createSondaEntry()));
      document.getElementById('addDroga').addEventListener('click', () => elements.drogasContainer.appendChild(createDrogaEntry()));
      document.getElementById('addSedacao').addEventListener('click', () => elements.sedacaoContainer.appendChild(createMedicationEntry('sedacao')));
      document.getElementById('addAnalgesia').addEventListener('click', () => elements.analgesiaContainer.appendChild(createMedicationEntry('analgesia')));
      document.getElementById('addAntibiotico').addEventListener('click', () => elements.antibioticosContainer.appendChild(createAntibioticoEntry()));

      // Event Listeners para verificações condicionais
      elements.dataNascimento.addEventListener('change', calcularIdade);

      elements.dataInternacao.addEventListener('change', function() {
        const dataInternacao = new Date(this.value);
        const dataPreenchimento = new Date(elements.dataPreenchimento.value);
        
        if (this.value && elements.dataPreenchimento.value) {
          const diffDias = calculateDays(dataInternacao, dataPreenchimento);
          elements.tempoInternacao.value = `${diffDias} dia(s)`;
        }
        
        formState.isDirty = true;
      });

      elements.dataPreenchimento.addEventListener('change', function() {
        const dataInternacao = new Date(elements.dataInternacao.value);
        const dataPreenchimento = new Date(this.value);
        
        if (elements.dataInternacao.value && this.value) {
          const diffDias = calculateDays(dataInternacao, dataPreenchimento);
          elements.tempoInternacao.value = `${diffDias} dia(s)`;
        }
        
        formState.isDirty = true;
      });

      elements.viaAlimentacao.addEventListener('change', function() {
        elements.quantidadeContainer.classList.toggle('hidden', 
          !['SNG', 'SNE', 'Gastrostomia', 'Jejunostomia'].includes(this.value));
          
        formState.isDirty = true;
      });

      elements.pacienteIntubado.addEventListener('change', function() {
        elements.intubacaoDetails.classList.toggle('hidden', this.value !== 'Sim');
        if (this.value !== 'Sim') {
          elements.dataIntubacao.value = '';
          limparCamposIntubacao();
          elements.modoVentilacao.value = '';
          elements.ventilacaoParametros.classList.add('hidden');
          elements.psvDetails.classList.add('hidden');
        }
        
        formState.isDirty = true;
      });

      elements.modoVentilacao.addEventListener('change', function() {
        elements.ventilacaoParametros.classList.toggle('hidden', !this.value);
        elements.psvDetails.classList.toggle('hidden', this.value !== 'PSV');
        formState.isDirty = true;
      });

      elements.dataIntubacao.addEventListener('change', function() {
        calcularTempoIntubacao();
        formState.isDirty = true;
      });

      elements.realizouTraqueostomia.addEventListener('change', function() {
        elements.dataTraqueostomiaContainer.classList.toggle('hidden', !this.checked);
        if (!this.checked) {
          elements.dataTraqueostomia.value = '';
        }
        
        formState.isDirty = true;
      });

      elements.dataTraqueostomia.addEventListener('change', function() {
        if (!this.value) return;
        
        const dataTraq = new Date(this.value);
        const dataInt = new Date(elements.dataIntubacao.value);
        const agora = new Date();
        
        if (dataTraq > agora) {
          showToast('A data da traqueostomia não pode ser no futuro', 5000);
          this.value = '';
          return;
        }
        
        if (dataInt && dataTraq < dataInt) {
          showToast('A data da traqueostomia não pode ser anterior à data de intubação', 5000);
          this.value = '';
        }
        
        formState.isDirty = true;
      });

      elements.dataUltimaEvacuacao.addEventListener('change', function() {
        calcularTempoDesdeEvacuacao();
        formState.isDirty = true;
      });

      elements.usoProtecaoGastrica.addEventListener('change', function() {
        elements.protecaoGastricaDetails.classList.toggle('hidden', this.value !== 'Sim');
        if (this.value !== 'Sim') {
          elements.tipoProtecaoGastrica.value = '';
        }
        
        formState.isDirty = true;
      });

      elements.usoTrombofilaxia.addEventListener('change', function() {
        elements.trombofilaxiaDetails.classList.toggle('hidden', this.value !== 'Sim');
        if (this.value !== 'Sim') {
          elements.tipoTrombofilaxia.value = '';
        }
        
        formState.isDirty = true;
      });

      // Manipuladores para campos básicos (marcar formulário como alterado)
      document.querySelectorAll('#roundMatinalForm input, #roundMatinalForm select, #roundMatinalForm textarea').forEach(input => {
        input.addEventListener('change', () => {
          formState.isDirty = true;
        });
      });

      // Manipuladores para botões de ação
      elements.saveData.addEventListener('click', savePatient);

      elements.exportarCSV.addEventListener('click', function() {
        try {
          if (!validateForm()) {
            showToast('Por favor, preencha todos os campos obrigatórios para exportar', 5000);
            return;
          }
          
          const formData = new FormData(document.getElementById('roundMatinalForm'));
          const dados = {};
          
          for (const [key, value] of formData.entries()) {
            dados[key] = value;
          }
          
          dados.timestamp = new Date().toISOString();
          
          const headers = Object.keys(dados);
          const csvContent = [
            headers.join(','),
            headers.map(header => {
              // Colocar aspas duplas ao redor de valores que contêm vírgulas ou novas linhas
              const val = dados[header] || '';
              if (val.includes(',') || val.includes('\n') || val.includes('"')) {
                return `"${val.replace(/"/g, '""')}"`;
              }
              return val;
            }).join(',')
          ].join('\n');

          // Criar um objeto Blob e um link para download
          const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
          const url = URL.createObjectURL(blob);
          const link = document.createElement('a');
          
          link.setAttribute('href', url);
          link.setAttribute('download', 'round_matinal_' + new Date().toISOString().slice(0,10) + '.csv');
          link.style.visibility = 'hidden';
          
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
          
          showToast('CSV exportado com sucesso!', 3000);
        } catch (error) {
          console.error("Erro ao exportar CSV:", error);
          showToast('Erro ao exportar CSV: ' + error.message, 5000);
        }
      });

      elements.exportarPDF.addEventListener('click', function() {
        // Mostrar ao usuário como salvar usando funcionalidade nativa do navegador
        showToast('Use a função de impressão do navegador (Ctrl+P ou no iOS: compartilhar -> imprimir) para salvar como PDF', 6000);
        
        // Criar versão de impressão
        const resumoContent = document.getElementById('resumoContent');
        if (resumoContent.children.length <= 1) {
          // Se o resumo ainda não foi gerado
          showToast('Gerando resumo para exportação...', 3000);
          generateSummary();
        }
        
        // Atrasar um pouco para dar tempo de gerar o resumo
        setTimeout(() => {
          window.print();
        }, 1000);
      });

      elements.clearForm.addEventListener('click', function() {
        if (confirm('Tem certeza de que deseja limpar todos os dados do formulário?')) {
          resetForm();
          
          // Configurar data de preenchimento para hoje
          elements.dataPreenchimento.valueAsDate = new Date();
          
          // Voltar para a primeira aba
          showTab('identificacao');
          
          // Se for um novo paciente, gerar novo ID
          if (formState.isNewPatient) {
            currentPatientId = generateId();
          }
          
          formState.isDirty = true;
          
          showToast('Formulário limpo com sucesso!', 3000);
        }
      });

      // Inicializações
      atualizarDataMaxima();
      
      // Atualizações automáticas para cálculos de tempo
      setInterval(() => {
        if (elements.dataIntubacao && elements.dataIntubacao.value) {
          calcularTempoIntubacao();
        }
        
        if (elements.dataUltimaEvacuacao && elements.dataUltimaEvacuacao.value) {
          calcularTempoDesdeEvacuacao();
        }
        
        // Atualizar tempos de uso de cateteres
        document.querySelectorAll('.data-insercao-cateter').forEach(input => {
          if (input.value) {
            const tempoUsoInput = input.closest('.medication-entry').querySelector('.tempo-uso-cateter');
            calcularTempoUso(input, tempoUsoInput);
          }
        });
        
        // Atualizar tempos de uso de antibióticos
        document.querySelectorAll('.data-inicio-antibiotico').forEach(input => {
          if (input.value) {
            const tempoUsoInput = input.closest('.medication-entry').querySelector('.tempo-uso-antibiotico');
            calcularTempoUsoAntibiotico(input, tempoUsoInput);
          }
        });
      }, 60000); // Atualizar a cada minuto
      
      // Atualizar datas máximas periodicamente
      setInterval(atualizarDataMaxima, 60000);
      
      // Inicializar banco de dados
      initDatabase();
    });
  </script>
</body>
</html>
