<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistema de Acompanhamento de Pacientes</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <style>
    /* CSS mantido igual para reduzir o tamanho */
    :root {
      --primary-color: #5D5CDE;
      --secondary-color: #8382eb;
      --success-color: #28a745;
      --danger-color: #dc3545;
      --warning-color: #ffc107;
      --info-color: #17a2b8;
      --border-radius: 0.5rem;
      --transition-speed: 0.3s;
    }
    
    /* Dark mode variables */
    @media (prefers-color-scheme: dark) {
      :root {
        --bg-color: #181818;
        --text-color: #f0f0f0;
        --card-bg: #2a2a2a;
        --border-color: #444;
        --input-bg: #333;
        --hover-bg: #333;
        --table-hover: rgba(255, 255, 255, 0.05);
        --table-header-bg: rgba(93, 92, 222, 0.2);
        --shadow-color: rgba(0, 0, 0, 0.3);
        --toast-bg: #2a2a2a;
      }
    }

    /* Light mode variables */
    @media (prefers-color-scheme: light) {
      :root {
        --bg-color: #FFFFFF;
        --text-color: #333333;
        --card-bg: #FFFFFF;
        --border-color: #e0e0e0;
        --input-bg: #f9f9f9;
        --hover-bg: #f5f5f5;
        --table-hover: rgba(0, 0, 0, 0.03);
        --table-header-bg: rgba(93, 92, 222, 0.1);
        --shadow-color: rgba(0, 0, 0, 0.1);
        --toast-bg: white;
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
      min-height: 100vh;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 1rem;
    }

    .card {
      background-color: var(--card-bg);
      border-radius: var(--border-radius);
      box-shadow: 0 4px 6px var(--shadow-color);
      padding: 1.5rem;
      margin-bottom: 1.5rem;
      border: 1px solid var(--border-color);
      transition: box-shadow 0.3s ease, transform 0.2s ease;
    }

    .card:hover {
      box-shadow: 0 6px 12px var(--shadow-color);
    }

    h1, h2, h3, h4, h5, h6 {
      color: var(--text-color);
      margin-bottom: 1rem;
      font-weight: 600;
    }
    
    h1 {
      font-size: 1.8rem;
      border-bottom: 2px solid var(--primary-color);
      padding-bottom: 0.5rem;
      display: inline-block;
    }
    
    h2 {
      font-size: 1.5rem;
      color: var(--primary-color);
    }
    
    h3 {
      font-size: 1.3rem;
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
      box-shadow: 0 2px 4px var(--shadow-color);
    }
    
    .btn:active {
      transform: translateY(1px);
      box-shadow: 0 1px 2px var(--shadow-color);
    }

    .btn-primary {
      background-color: var(--primary-color);
      color: white;
    }

    .btn-primary:hover {
      background-color: #4a49b9;
    }

    .btn-secondary {
      background-color: #6c757d;
      color: white;
    }
    
    .btn-secondary:hover {
      background-color: #5a6268;
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
    
    .btn-info {
      background-color: var(--info-color);
      color: white;
    }
    
    .btn-info:hover {
      background-color: #138496;
    }
    
    .btn i {
      margin-right: 0.5rem;
    }

    .btn-sm {
      padding: 0.25rem 0.5rem;
      font-size: 0.875rem;
      min-height: 2rem;
    }
    
    .btn-lg {
      padding: 0.75rem 1.5rem;
      font-size: 1.25rem;
      min-height: 3rem;
    }

    .btn-group {
      display: flex;
      gap: 0.5rem;
      margin-top: 1rem;
      flex-wrap: wrap;
    }

    .form-group {
      margin-bottom: 1.25rem;
    }

    .form-control {
      width: 100%;
      padding: 0.75rem;
      border: 1px solid var(--border-color);
      border-radius: 0.25rem;
      font-size: 1rem;
      transition: all 0.2s ease-in-out;
      background-color: var(--input-bg);
      color: var(--text-color);
    }

    .form-control:focus {
      border-color: var(--primary-color);
      outline: none;
      box-shadow: 0 0 0 3px rgba(93, 92, 222, 0.25);
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
      display: none;
    }
    
    .invalid + .validation-message {
      display: block;
    }

    .alert {
      padding: 1rem;
      border-radius: 0.25rem;
      margin-bottom: 1rem;
      border-left: 4px solid transparent;
    }

    .alert-warning {
      background-color: rgba(255, 193, 7, 0.2);
      border-left-color: var(--warning-color);
      color: #856404;
    }

    .alert-danger {
      background-color: rgba(220, 53, 69, 0.2);
      border-left-color: var(--danger-color);
      color: #721c24;
    }
    
    .alert-success {
      background-color: rgba(40, 167, 69, 0.2);
      border-left-color: var(--success-color);
      color: #155724;
    }
    
    .alert-info {
      background-color: rgba(23, 162, 184, 0.2);
      border-left-color: var(--info-color);
      color: #0c5460;
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

    .daily-entry {
      border: 1px solid var(--border-color);
      border-radius: 0.25rem;
      padding: 1rem;
      margin-bottom: 1rem;
      background-color: var(--card-bg);
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }
    
    .daily-entry:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 8px var(--shadow-color);
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
      user-select: none;
    }

    .tab.active {
      color: var(--primary-color);
      border-bottom: 2px solid var(--primary-color);
    }
    
    .tab:hover:not(.active) {
      background-color: var(--hover-bg);
    }

    .tab-content {
      display: none;
      animation: fadeIn 0.3s ease forwards;
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
      background-color: var(--toast-bg);
      color: var(--text-color);
      border-radius: 0.25rem;
      box-shadow: 0 4px 6px var(--shadow-color);
      opacity: 0;
      transition: opacity 0.3s ease, transform 0.3s ease;
      z-index: 1000;
      max-width: 90%;
      border-left: 4px solid var(--primary-color);
      transform: translateY(-10px);
    }

    .toast.show {
      opacity: 1;
      transform: translateY(0);
    }
    
    .toast.success {
      border-left-color: var(--success-color);
    }
    
    .toast.error {
      border-left-color: var(--danger-color);
    }
    
    .toast.warning {
      border-left-color: var(--warning-color);
    }

    @media (max-width: 768px) {
      .flex-container {
        flex-direction: column;
      }
      
      .flex-container > div {
        width: 100%;
      }
      
      .btn-group {
        flex-direction: column;
      }
      
      .btn {
        width: 100%;
        margin-bottom: 0.5rem;
      }
      
      .card {
        padding: 1rem;
      }
      
      .container {
        padding: 0.5rem;
      }
      
      h1 {
        font-size: 1.5rem;
      }
      
      h2 {
        font-size: 1.3rem;
      }
    }

    /* Estilos para tabela de resumo */
    .table-container {
      overflow-x: auto;
      margin-bottom: 1.5rem;
      border-radius: var(--border-radius);
      border: 1px solid var(--border-color);
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 0;
    }

    th, td {
      padding: 0.75rem;
      text-align: left;
      border-bottom: 1px solid var(--border-color);
    }

    th {
      background-color: var(--table-header-bg);
      font-weight: 600;
      position: sticky;
      top: 0;
    }

    tr:hover {
      background-color: var(--table-hover);
    }
    
    tr:last-child td {
      border-bottom: none;
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
    
    @keyframes slideIn {
      from { transform: translateY(20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
    
    .slide-in {
      animation: slideIn 0.3s ease forwards;
    }
    
    /* Modal */
    .modal {
      display: none;
      position: fixed;
      z-index: 9999;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.6);
      padding: 20px;
      overflow-y: auto;
    }
    
    .modal-content {
      background-color: var(--card-bg);
      margin: 20px auto;
      padding: 20px;
      width: 90%;
      max-width: 600px;
      border-radius: var(--border-radius);
      box-shadow: 0 4px 8px var(--shadow-color);
      position: relative;
    }
    
    .modal-header {
      margin-bottom: 20px;
    }
    
    .modal-close {
      position: absolute;
      right: 15px;
      top: 15px;
      font-size: 24px;
      cursor: pointer;
      color: var(--text-color);
      background: none;
      border: none;
      width: 30px;
      height: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
    }
    
    .modal-close:hover {
      background-color: var(--hover-bg);
    }
    
    /* Lista de pacientes */
    .patient-card {
      padding: 1rem;
      border: 1px solid var(--border-color);
      border-radius: 0.25rem;
      margin-bottom: 0.5rem;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    
    .patient-card:hover {
      background-color: rgba(93, 92, 222, 0.1);
      transform: translateX(3px);
    }
    
    .patient-card.selected {
      background-color: rgba(93, 92, 222, 0.2);
      border-color: var(--primary-color);
    }
    
    .patient-info {
      flex: 1;
    }
    
    .patient-actions {
      display: flex;
      gap: 0.5rem;
    }
    
    .patient-actions button {
      padding: 0.25rem 0.5rem;
      font-size: 0.875rem;
    }
    
    .patient-record {
      font-size: 0.875rem;
      color: var(--text-color);
      opacity: 0.7;
    }
    
    .patient-name {
      font-weight: 600;
      margin-bottom: 0.25rem;
    }
    
    .badge {
      display: inline-block;
      padding: 0.25rem 0.5rem;
      font-size: 0.75rem;
      font-weight: 600;
      border-radius: 9999px;
      margin-left: 0.5rem;
    }
    
    .badge-primary {
      background-color: var(--primary-color);
      color: white;
    }
    
    .badge-success {
      background-color: var(--success-color);
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
    
    .badge-info {
      background-color: var(--info-color);
      color: white;
    }
    
    .badge-secondary {
      background-color: #6c757d;
      color: white;
    }
    
    /* Campos de entrada aprimorados */
    .input-group {
      display: flex;
      align-items: stretch;
    }
    
    .input-group .form-control {
      flex: 1;
      border-top-right-radius: 0;
      border-bottom-right-radius: 0;
    }
    
    .input-group-append {
      display: flex;
    }
    
    .input-group-text {
      display: flex;
      align-items: center;
      padding: 0.75rem;
      border: 1px solid var(--border-color);
      border-left: 0;
      background-color: var(--input-bg);
      border-top-right-radius: 0.25rem;
      border-bottom-right-radius: 0.25rem;
      color: var(--text-color);
    }
    
    /* Separador */
    .divider {
      height: 1px;
      background-color: var(--border-color);
      margin: 1.5rem 0;
    }
    
    /* Cabeçalho da página */
    .page-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
      flex-wrap: wrap;
      gap: 1rem;
    }
    
    @media (max-width: 768px) {
      .page-header {
        flex-direction: column;
        align-items: flex-start;
      }
    }
    
    /* Badge para alta */
    .discharge-badge {
      background-color: #28a745;
      color: white;
      padding: 0.25rem 0.5rem;
      border-radius: 9999px;
      font-size: 0.75rem;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
    }
    
    .discharge-badge i {
      margin-right: 0.25rem;
    }
    
    /* Empty state */
    .empty-state {
      text-align: center;
      padding: 2rem;
      color: var(--text-color);
      opacity: 0.6;
    }
    
    .empty-state i {
      font-size: 3rem;
      margin-bottom: 1rem;
      opacity: 0.3;
    }
    
    .empty-state-text {
      font-size: 1.2rem;
      margin-bottom: 1rem;
    }
    
    /* Toggle switch */
    .switch {
      position: relative;
      display: inline-block;
      width: 50px;
      height: 24px;
      margin-right: 0.5rem;
    }
    
    .switch input {
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
      background-color: #ccc;
      transition: .4s;
      border-radius: 24px;
    }
    
    .slider:before {
      position: absolute;
      content: "";
      height: 16px;
      width: 16px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }
    
    input:checked + .slider {
      background-color: var(--primary-color);
    }
    
    input:focus + .slider {
      box-shadow: 0 0 1px var(--primary-color);
    }
    
    input:checked + .slider:before {
      transform: translateX(26px);
    }
    
    .switch-container {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
    }
    
    /* Required field indicator */
    .required-field::after {
      content: "*";
      color: var(--danger-color);
      margin-left: 4px;
    }
    
    /* Gráficos */
    .chart-container {
      position: relative;
      height: 300px;
      margin-bottom: 2rem;
    }
    
    /* Histórico de registros */
    .history-timeline {
      position: relative;
      margin-left: 1.5rem;
      padding-left: 1.5rem;
    }
    
    .history-timeline::before {
      content: '';
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      width: 2px;
      background-color: var(--border-color);
    }
    
    .history-item {
      position: relative;
      margin-bottom: 1.5rem;
    }
    
    .history-item::before {
      content: '';
      position: absolute;
      left: -1.5rem;
      top: 0.5rem;
      width: 1rem;
      height: 1rem;
      border-radius: 50%;
      background-color: var(--primary-color);
    }
    
    .history-item .history-date {
      font-weight: 600;
      margin-bottom: 0.5rem;
      color: var(--primary-color);
    }
    
    .history-content {
      background-color: var(--card-bg);
      border: 1px solid var(--border-color);
      border-radius: 0.25rem;
      padding: 1rem;
    }
    

    
    /* Novo indicador visual de que o paciente está selecionado */
    .patient-selected-indicator {
      padding: 0.5rem;
      background-color: rgba(93, 92, 222, 0.1);
      border-radius: 0.25rem;
      border-left: 4px solid var(--primary-color);
      margin-bottom: 1rem;
      animation: pulse 2s infinite;
    }
    
    @keyframes pulse {
      0% {
        box-shadow: 0 0 0 0 rgba(93, 92, 222, 0.4);
      }
      70% {
        box-shadow: 0 0 0 10px rgba(93, 92, 222, 0);
      }
      100% {
        box-shadow: 0 0 0 0 rgba(93, 92, 222, 0);
      }
    }
    
    /* Novo estilo para o botão de ação flutuante */
    .floating-action-button {
      position: fixed;
      bottom: 2rem;
      right: 2rem;
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background-color: var(--primary-color);
      color: white;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      z-index: 100;
      transition: all 0.3s ease;
    }
    
    .floating-action-button:hover {
      transform: scale(1.1);
      background-color: #4a49b9;
    }
    
    .floating-action-button i {
      font-size: 24px;
      margin: 0;
    }
    
    /* Estilos para a caixa de dica sobre o botão flutuante */
    .fab-tooltip {
      position: absolute;
      right: 70px;
      background-color: rgba(0,0,0,0.8);
      color: white;
      padding: 5px 10px;
      border-radius: 4px;
      font-size: 14px;
      opacity: 0;
      transition: opacity 0.3s;
      pointer-events: none;
      white-space: nowrap;
    }
    
    .floating-action-button:hover .fab-tooltip {
      opacity: 1;
    }
    
    /* Estilo para o botão grande de novo registro */
    .big-action-button {
      background-color: var(--primary-color);
      border-radius: var(--border-radius);
      color: white;
      padding: 1.5rem;
      text-align: center;
      margin: 2rem auto;
      cursor: pointer;
      transition: all 0.3s ease;
      max-width: 400px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    
    .big-action-button:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 15px rgba(0,0,0,0.15);
      background-color: #4a49b9;
    }
    
    .big-action-button i {
      font-size: 2rem;
      margin-bottom: 1rem;
      display: block;
    }
    
    .big-action-button-text {
      font-size: 1.2rem;
      font-weight: 600;
    }
    
    /* Estilo para o botão destacado de novo registro */
    .highlight-btn {
      position: relative;
      overflow: hidden;
      background-color: var(--primary-color);
    }
    
    .highlight-btn::after {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: linear-gradient(to bottom right, 
                                 rgba(255,255,255,0) 0%, 
                                 rgba(255,255,255,0.1) 50%, 
                                 rgba(255,255,255,0) 100%);
      transform: rotate(45deg);
      animation: highlight-shine 3s infinite;
    }
    
    @keyframes highlight-shine {
      0% {
        transform: translateX(-100%) rotate(45deg);
      }
      100% {
        transform: translateX(100%) rotate(45deg);
      }
    }
    
    /* Cores para indicadores de tempo */
    .text-success {
      color: var(--success-color);
    }
    
    .text-warning {
      color: var(--warning-color);
    }
    
    .text-danger {
      color: var(--danger-color);
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="page-header">
      <h1>Sistema de Acompanhamento de Pacientes</h1>
      <div class="btn-group">
        <button id="newPatientBtn" class="btn btn-primary" onclick="showModal('patientModal')">
          <i class="fas fa-user-plus"></i> Novo Paciente
        </button>
        <button id="exportAllBtn" class="btn btn-success">
          <i class="fas fa-file-export"></i> Exportar Dados
        </button>
      </div>
    </div>
    

    
    <div class="card">
      <div class="search-container">
        <i class="fas fa-search search-icon"></i>
        <input type="text" id="searchPatients" class="form-control" placeholder="Buscar pacientes...">
      </div>
      
      <div class="sticky-tabs tabs">
        <div class="tab active" data-tab="patientList" onclick="manualTabSwitch('patientList')">Lista de Pacientes</div>
        <div class="tab" data-tab="patientDetails" onclick="manualTabSwitch('patientDetails')">Detalhes do Paciente</div>
        <div class="tab" data-tab="dailyRecord" onclick="manualTabSwitch('dailyRecord')">Registro Diário</div>
        <div class="tab" data-tab="patientHistory" onclick="manualTabSwitch('patientHistory')">Histórico</div>
        <div class="tab" data-tab="patientStats" onclick="manualTabSwitch('patientStats')">Estatísticas</div>
      </div>
      
      <!-- Indicador de paciente selecionado -->
      <div id="patientSelectedIndicator" class="patient-selected-indicator" style="display:none">
        <div style="display: flex; justify-content: space-between; align-items: center;">
          <div>
            <i class="fas fa-user-check"></i> Paciente Selecionado: <span id="selectedPatientName">-</span>
          </div>
          <!-- NOVO: Botão de novo registro diretamente no indicador -->
          <button id="quickNewRecordBtn" class="btn btn-primary btn-sm highlight-btn" onclick="createNewDailyRecord()">
            <i class="fas fa-plus"></i> Novo Registro
          </button>
        </div>
      </div>
      
      <div id="patientList" class="tab-content active">
        <div class="filter-options">
          <div class="flex-container">
            <div>
              <div class="form-group">
                <label for="statusFilter" class="form-label">Filtrar por Status</label>
                <select id="statusFilter" class="form-control">
                  <option value="all">Todos</option>
                  <option value="active">Internados</option>
                  <option value="discharged">Alta</option>
                </select>
              </div>
            </div>
            <div>
              <div class="form-group">
                <label for="sortPatients" class="form-label">Ordenar por</label>
                <select id="sortPatients" class="form-control">
                  <option value="nameAsc">Nome (A-Z)</option>
                  <option value="nameDesc">Nome (Z-A)</option>
                  <option value="dateAsc">Data Internação (antiga-recente)</option>
                  <option value="dateDesc">Data Internação (recente-antiga)</option>
                </select>
              </div>
            </div>
          </div>
        </div>
        
        <div id="patientListContainer">
          <!-- Lista de pacientes será carregada aqui -->
        </div>
        
        <div class="empty-state" id="emptyPatientList">
          <i class="fas fa-user-injured"></i>
          <div class="empty-state-text">Nenhum paciente cadastrado</div>
          <button class="btn btn-primary" onclick="showModal('patientModal')">
            <i class="fas fa-user-plus"></i> Adicionar paciente
          </button>
        </div>
      </div>
      
      <div id="patientDetails" class="tab-content">
        <div id="selectedPatientDetails">
          <!-- Detalhes do paciente serão carregados aqui -->
          <div class="empty-state" id="emptyPatientDetails">
            <i class="fas fa-user"></i>
            <div class="empty-state-text">Selecione um paciente para visualizar os detalhes</div>
            <p>Vá para a aba "Lista de Pacientes" e selecione um paciente.</p>
          </div>
        </div>
        
        <!-- NOVO: Botão de ações mais prominente -->
        <div id="patientActions" class="btn-group hidden">
          <button id="editPatientBtn" class="btn btn-info">
            <i class="fas fa-edit"></i> Editar
          </button>
          <button id="newDailyRecordBtn" class="btn btn-primary highlight-btn" onclick="createNewDailyRecord()">
            <i class="fas fa-notes-medical"></i> Novo Registro
          </button>
          <button id="dischargePatientBtn" class="btn btn-success">
            <i class="fas fa-check-circle"></i> Alta Hospitalar
          </button>
          <button id="deletePatientBtn" class="btn btn-danger">
            <i class="fas fa-trash-alt"></i> Excluir
          </button>
        </div>
      </div>
      
      <div id="dailyRecord" class="tab-content">
        <!-- NOVO: Botão grande para criar novo registro quando não há um formulário aberto -->
        <div id="newRecordButtonContainer" class="big-action-button" onclick="createNewDailyRecord()">
          <i class="fas fa-plus-circle"></i>
          <div class="big-action-button-text">Criar Novo Registro Diário</div>
          <p>Clique aqui para adicionar um novo registro para o paciente selecionado</p>
        </div>
        
        <div id="dailyRecordForm" class="hidden">
          <h2>Novo Registro Diário</h2>
          <p>Adicionando registro para: <strong id="currentPatientName">-</strong></p>
          
          <form id="recordForm">
            <div class="flex-container">
              <div>
                <div class="form-group">
                  <label for="recordDate" class="form-label required-field">Data</label>
                  <input type="date" id="recordDate" class="form-control" required>
                  <div class="validation-message">Data é obrigatória</div>
                </div>
              </div>
              <div>
                <div class="form-group">
                  <label for="recordTime" class="form-label required-field">Hora</label>
                  <input type="time" id="recordTime" class="form-control" required>
                  <div class="validation-message">Hora é obrigatória</div>
                </div>
              </div>
            </div>
            
            <div class="form-group">
              <label class="form-label required-field" id="vitalSigns">Sinais Vitais</label>
              <div class="flex-container">
                <div>
                  <div class="form-group">
                    <label for="temperature" class="form-label">Temperatura (°C)</label>
                    <div class="input-group">
                      <input type="number" id="temperature" class="form-control" step="0.1" min="35" max="42">
                      <div class="input-group-append">
                        <span class="input-group-text">°C</span>
                      </div>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="form-group">
                    <label for="heartRate" class="form-label">Freq. Cardíaca</label>
                    <div class="input-group">
                      <input type="number" id="heartRate" class="form-control" step="1" min="40" max="200">
                      <div class="input-group-append">
                        <span class="input-group-text">bpm</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="flex-container">
                <div>
                  <div class="form-group">
                    <label for="bloodPressure" class="form-label">Pressão Arterial</label>
                    <div class="input-group">
                      <input type="text" id="bloodPressure" class="form-control" placeholder="120/80">
                      <div class="input-group-append">
                        <span class="input-group-text">mmHg</span>
                      </div>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="form-group">
                    <label for="respiratoryRate" class="form-label">Freq. Respiratória</label>
                    <div class="input-group">
                      <input type="number" id="respiratoryRate" class="form-control" step="1" min="8" max="40">
                      <div class="input-group-append">
                        <span class="input-group-text">irpm</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="flex-container">
                <div>
                  <div class="form-group">
                    <label for="oxygenSaturation" class="form-label">Saturação O₂</label>
                    <div class="input-group">
                      <input type="number" id="oxygenSaturation" class="form-control" step="1" min="70" max="100">
                      <div class="input-group-append">
                        <span class="input-group-text">%</span>
                      </div>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="form-group">
                    <label for="painLevel" class="form-label">Nível de Dor (0-10)</label>
                    <input type="range" id="painLevel" class="form-control" min="0" max="10" step="1" value="0">
                    <div id="painLevelValue" class="text-center">0 - Sem dor</div>
                  </div>
                </div>
              </div>
              <div class="validation-message">Pelo menos um sinal vital deve ser preenchido</div>
            </div>
            
            <div class="form-group">
              <label for="medications" class="form-label">Antibioticoterapia</label>
              <div id="medicationsList">
                <div class="medication-entry">
                  <div class="flex-container">
                    <div>
                      <div class="form-group">
                        <label for="medicationName" class="form-label">Nome</label>
                        <input type="text" id="medicationName" class="form-control medication-name">
                      </div>
                    </div>
                    <div>
                      <div class="form-group">
                        <label for="medicationDose" class="form-label">Dose</label>
                        <input type="text" id="medicationDose" class="form-control medication-dose">
                      </div>
                    </div>
                  </div>
                  <div class="flex-container">
                    <div>
                      <div class="form-group">
                        <label for="medicationStartDate" class="form-label">Data de Início</label>
                        <input type="date" id="medicationStartDate" class="form-control medication-start-date">
                      </div>
                    </div>
                    <div>
                      <div class="form-group">
                        <label for="medicationRoute" class="form-label">Via de Administração</label>
                        <select id="medicationRoute" class="form-control medication-route">
                          <option value="">Selecione</option>
                          <option value="Oral">Oral</option>
                          <option value="Intravenosa">Intravenosa</option>
                          <option value="Intramuscular">Intramuscular</option>
                          <option value="Subcutânea">Subcutânea</option>
                          <option value="Inalatória">Inalatória</option>
                          <option value="Tópica">Tópica</option>
                          <option value="Outras">Outras</option>
                        </select>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <button type="button" id="addMedicationBtn" class="btn btn-sm btn-secondary mt-2">
                <i class="fas fa-plus"></i> Adicionar Antibiótico
              </button>
            </div>
            
            <div class="form-group">
              <label for="procedures" class="form-label">Procedimentos Realizados</label>
              <textarea id="procedures" class="form-control" rows="2"></textarea>
            </div>
            
            <div class="form-group">
              <label for="observations" class="form-label">Observações Clínicas</label>
              <textarea id="observations" class="form-control notes-field"></textarea>
            </div>
            
            <div class="form-group">
              <label for="nutritionalStatus" class="form-label">Estado Nutricional</label>
              <select id="nutritionalStatus" class="form-control">
                <option value="">Selecione</option>
                <option value="Adequado">Adequado</option>
                <option value="Inapetente">Inapetente</option>
                <option value="Desnutrido">Desnutrido</option>
                <option value="Obeso">Obeso</option>
                <option value="NPO">NPO (Nada por via oral)</option>
                <option value="Dieta Especial">Dieta Especial</option>
              </select>
            </div>
            
            <div class="form-group">
              <label for="mobilityStatus" class="form-label">Mobilidade</label>
              <select id="mobilityStatus" class="form-control">
                <option value="">Selecione</option>
                <option value="Deambula sem auxílio">Deambula sem auxílio</option>
                <option value="Deambula com auxílio">Deambula com auxílio</option>
                <option value="Restrito ao leito">Restrito ao leito</option>
                <option value="Restrito à cadeira">Restrito à cadeira</option>
                <option value="Mobilidade prejudicada">Mobilidade prejudicada</option>
              </select>
            </div>
            
            <div class="form-group">
              <div class="switch-container">
                <label class="switch">
                  <input type="checkbox" id="isIntubated">
                  <span class="slider"></span>
                </label>
                <label for="isIntubated">Paciente Intubado</label>
              </div>
            </div>
            
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
                
                <div class="flex-container">
                  <div>
                    <div class="form-group">
                      <label for="ventilationMode" class="form-label">Modo de Ventilação</label>
                      <select id="ventilationMode" class="form-control">
                        <option value="">Selecione</option>
                        <option value="PCV">PCV</option>
                        <option value="VCV">VCV</option>
                        <option value="PSV">PSV</option>
                      </select>
                    </div>
                  </div>
                  <div>
                    <div class="form-group">
                      <label for="fio2" class="form-label">FiO2 (%)</label>
                      <div class="input-group">
                        <input type="number" id="fio2" class="form-control" min="21" max="100">
                        <div class="input-group-append">
                          <span class="input-group-text">%</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div class="flex-container">
                  <div>
                    <div class="form-group">
                      <label for="vc" class="form-label">VC (Volume Corrente)</label>
                      <div class="input-group">
                        <input type="number" id="vc" class="form-control">
                        <div class="input-group-append">
                          <span class="input-group-text">ml</span>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div>
                    <div class="form-group">
                      <label for="vt" class="form-label">VT (Volume Total)</label>
                      <div class="input-group">
                        <input type="number" id="vt" class="form-control">
                        <div class="input-group-append">
                          <span class="input-group-text">L/min</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div class="flex-container">
                  <div>
                    <div class="form-group">
                      <label for="ventilatoryFrequency" class="form-label">FR (Frequência Respiratória)</label>
                      <div class="input-group">
                        <input type="number" id="ventilatoryFrequency" class="form-control" min="0" max="60">
                        <div class="input-group-append">
                          <span class="input-group-text">irpm</span>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div>
                    <div class="form-group">
                      <label for="peep" class="form-label">PEEP</label>
                      <div class="input-group">
                        <input type="number" id="peep" class="form-control" min="0" max="30">
                        <div class="input-group-append">
                          <span class="input-group-text">cmH₂O</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div class="flex-container">
                  <div>
                    <div class="form-group">
                      <label for="inspiratoryPressure" class="form-label">Pressão Inspiratória</label>
                      <div class="input-group">
                        <input type="number" id="inspiratoryPressure" class="form-control">
                        <div class="input-group-append">
                          <span class="input-group-text">cmH₂O</span>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div>
                    <div class="form-group">
                      <label for="peakPressure" class="form-label">Pressão de Pico</label>
                      <div class="input-group">
                        <input type="number" id="peakPressure" class="form-control">
                        <div class="input-group-append">
                          <span class="input-group-text">cmH₂O</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div class="flex-container">
                  <div>
                    <div class="form-group">
                      <label for="plateauPressure" class="form-label">Pressão de Platô</label>
                      <div class="input-group">
                        <input type="number" id="plateauPressure" class="form-control">
                        <div class="input-group-append">
                          <span class="input-group-text">cmH₂O</span>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div>
                    <!-- Espaço para balanceamento visual -->
                  </div>
                </div>
              </div>
              
              <div class="form-group">
                <label for="intubationNotes" class="form-label">Observações sobre intubação</label>
                <textarea id="intubationNotes" class="form-control notes-field" placeholder="Informe detalhes relevantes sobre a intubação ou condições respiratórias"></textarea>
              </div>
            </div>
            
            <div class="form-group">
              <div class="switch-container">
                <label class="switch">
                  <input type="checkbox" id="isUnderSedation">
                  <span class="slider"></span>
                </label>
                <label for="isUnderSedation">Paciente sob Sedação</label>
              </div>
            </div>
            
            <div id="sedationSection" class="hidden">
              <div class="alert alert-info">
                <i class="fas fa-info-circle"></i> Informações sobre sedação do paciente.
              </div>
              
              <div id="sedationsList">
                <div class="sedation-entry">
                  <div class="flex-container">
                    <div>
                      <div class="form-group">
                        <label for="sedationType" class="form-label">Tipo de Sedação</label>
                        <select class="form-control sedation-type">
                          <option value="">Selecione</option>
                          <option value="Midazolam">Midazolam</option>
                          <option value="Propofol">Propofol</option>
                          <option value="Ketamina">Ketamina</option>
                          <option value="Dexmedetomidina">Dexmedetomidina</option>
                          <option value="Outro">Outro</option>
                        </select>
                      </div>
                    </div>
                    <div>
                      <div class="form-group">
                        <label for="sedationDose" class="form-label">Dose</label>
                        <input type="text" class="form-control sedation-dose" placeholder="Ex: 5mg/h, 50mcg/kg/min">
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <button type="button" id="addSedationBtn" class="btn btn-sm btn-secondary mt-2">
                <i class="fas fa-plus"></i> Adicionar Sedação
              </button>
            </div>
            
            <div class="form-group">
              <div class="switch-container">
                <label class="switch">
                  <input type="checkbox" id="isUnderAnalgesia">
                  <span class="slider"></span>
                </label>
                <label for="isUnderAnalgesia">Paciente recebendo Analgesia</label>
              </div>
            </div>
            
            <div id="analgesiaSection" class="hidden">
              <div class="alert alert-info">
                <i class="fas fa-info-circle"></i> Informações sobre analgesia do paciente.
              </div>
              
              <div id="analgesiaList">
                <div class="analgesia-entry">
                  <div class="flex-container">
                    <div>
                      <div class="form-group">
                        <label for="analgesiaType" class="form-label">Tipo de Analgésico</label>
                        <select class="form-control analgesia-type">
                          <option value="">Selecione</option>
                          <option value="Fentanil">Fentanil</option>
                          <option value="Morfina">Morfina</option>
                          <option value="Codeína">Codeína</option>
                          <option value="Tramadol">Tramadol</option>
                          <option value="Dipirona">Dipirona</option>
                          <option value="Paracetamol">Paracetamol</option>
                          <option value="AINH">AINH</option>
                          <option value="Outro">Outro</option>
                        </select>
                      </div>
                    </div>
                    <div>
                      <div class="form-group">
                        <label for="analgesiaDaily" class="form-label">Dose Diária</label>
                        <input type="text" class="form-control analgesia-daily" placeholder="Ex: 50mg 6/6h, 1g 4x/dia">
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <button type="button" id="addAnalgesiaBtn" class="btn btn-sm btn-secondary mt-2">
                <i class="fas fa-plus"></i> Adicionar Analgésico
              </button>
            </div>
            
            <div class="form-group">
              <div class="switch-container">
                <label class="switch">
                  <input type="checkbox" id="isUnderVasopressors">
                  <span class="slider"></span>
                </label>
                <label for="isUnderVasopressors">Paciente recebendo Drogas Vasoativas (DVA)</label>
              </div>
            </div>
            
            <div id="vasopressorSection" class="hidden">
              <div class="alert alert-info">
                <i class="fas fa-info-circle"></i> Informações sobre drogas vasoativas do paciente.
              </div>
              
              <div id="vasopressorList">
                <div class="vasopressor-entry">
                  <div class="flex-container">
                    <div>
                      <div class="form-group">
                        <label for="vasopressorType" class="form-label">Tipo de Droga Vasoativa</label>
                        <select class="form-control vasopressor-type">
                          <option value="">Selecione</option>
                          <option value="Norepinefrina">Norepinefrina</option>
                          <option value="Adrenalina">Adrenalina</option>
                          <option value="Vasopressina">Vasopressina</option>
                          <option value="Dobutamina">Dobutamina</option>
                          <option value="Dopamina">Dopamina</option>
                          <option value="Outra">Outra</option>
                        </select>
                      </div>
                    </div>
                    <div>
                      <div class="form-group">
                        <label for="vasopressorDose" class="form-label">Dose (ml/h)</label>
                        <input type="text" class="form-control vasopressor-dose" placeholder="Ex: 5ml/h, 10ml/h">
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <button type="button" id="addVasopressorBtn" class="btn btn-sm btn-secondary mt-2">
                <i class="fas fa-plus"></i> Adicionar Droga Vasoativa
              </button>
            </div>
            
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
            
            <div class="form-group">
              <div class="switch-container">
                <label class="switch">
                  <input type="checkbox" id="dischargePatient">
                  <span class="slider"></span>
                </label>
                <label for="dischargePatient">Conceder Alta ao Paciente</label>
              </div>
            </div>
            
            <div id="dischargeSection" class="hidden">
              <div class="alert alert-info">
                <i class="fas fa-info-circle"></i> Preencha as informações de alta do paciente.
              </div>
              
              <div class="form-group">
                <label for="dischargeReason" class="form-label required-field">Motivo da Alta</label>
                <select id="dischargeReason" class="form-control">
                  <option value="">Selecione</option>
                  <option value="Melhora clínica">Melhora clínica</option>
                  <option value="A pedido">A pedido</option>
                  <option value="Transferência">Transferência</option>
                  <option value="Óbito">Óbito</option>
                  <option value="Evasão">Evasão</option>
                  <option value="Outro">Outro</option>
                </select>
                <div class="validation-message">Motivo da alta é obrigatório</div>
              </div>
              
              <div class="form-group">
                <label for="dischargeSummary" class="form-label required-field">Resumo da Alta</label>
                <textarea id="dischargeSummary" class="form-control notes-field"></textarea>
                <div class="validation-message">Resumo da alta é obrigatório</div>
              </div>
              
              <div class="form-group">
                <label for="followUpInstructions" class="form-label">Instruções de Acompanhamento</label>
                <textarea id="followUpInstructions" class="form-control notes-field"></textarea>
              </div>
            </div>
            
            <div class="btn-group">
              <button type="submit" id="saveRecordBtn" class="btn btn-primary">
                <i class="fas fa-save"></i> Salvar Registro
              </button>
              <button type="button" id="cancelRecordBtn" class="btn btn-secondary">
                <i class="fas fa-times"></i> Cancelar
              </button>
            </div>
          </form>
        </div>
        
        <div class="empty-state" id="dailyRecordEmptyState">
          <i class="fas fa-clipboard-list"></i>
          <div class="empty-state-text">Selecione um paciente e crie um novo registro diário</div>
          
          <!-- NOVO: Botão de ação na mensagem de estado vazio -->
          <button class="btn btn-primary" onclick="manualTabSwitch('patientList')">
            <i class="fas fa-users"></i> Ir para Lista de Pacientes
          </button>
        </div>
      </div>
      
      <div id="patientHistory" class="tab-content">
        <!-- Resto do conteúdo do histórico -->
      </div>
      
      <div id="patientStats" class="tab-content">
        <!-- Resto do conteúdo das estatísticas -->
      </div>
    </div>
    
    <!-- MODAIS -->
    <!-- Modal de Novo/Editar Paciente, etc. -->
  </div>

  <script>
    // Variáveis globais para armazenar os dados e estado da aplicação
    const appData = {
      patients: [],
      records: [],
      selectedPatientId: null,
      editingPatientId: null,
      editingRecordId: null,
      lastSelectedTabId: 'patientList'  // Armazena a última aba acessada pelo usuário
    };
    
    // Constante para mostrar/esconder o modo debug
    const DEBUG_MODE = false;
    
    document.addEventListener('DOMContentLoaded', function() {
      // Verificar o esquema de cores preferido
      if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
        document.documentElement.classList.add('dark');
      }
      window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
        if (event.matches) {
          document.documentElement.classList.add('dark');
        } else {
          document.documentElement.classList.remove('dark');
        }
      });
      
      // Carregar dados do localStorage
      loadDataFromStorage();
      
      // Inicializar pacientes de exemplo se necessário
      addSampleData();
      
      // Renderizar lista de pacientes
      renderPatientList();
      
      // Configurar eventos
      setupEventListeners();
      
      // Ativar a primeira aba
      manualTabSwitch('patientList');
      
      // Selecionar primeiro paciente por padrão (se existir algum)
      if (appData.patients.length > 0) {
        selectPatient(appData.patients[0].id);
        showToast('Paciente selecionado automaticamente!', 'info');
      }
      
      logDebug('Sistema inicializado com sucesso!');
    });
    
    // Configurar ouvintes de eventos
    function setupEventListeners() {
      // Formulário de paciente
      document.getElementById('patientForm').addEventListener('submit', savePatient);
      
      // Formulário de registro
      document.getElementById('recordForm').addEventListener('submit', saveRecord);
      
      // Evento de checkbox de alta
      document.getElementById('dischargePatient').addEventListener('change', function() {
        const dischargeSection = document.getElementById('dischargeSection');
        dischargeSection.classList.toggle('hidden', !this.checked);
      });
      
      // Evento de checkbox de intubação
      document.getElementById('isIntubated').addEventListener('change', function() {
        const intubationSection = document.getElementById('intubationSection');
        intubationSection.classList.toggle('hidden', !this.checked);
        
        // Se o checkbox for marcado, atualizar o cálculo de tempo
        if (this.checked) {
          updateIntubationDuration();
        }
      });
      
      // Evento de mudança de data de início da intubação
      document.getElementById('intubationStartDate').addEventListener('change', function() {
        updateIntubationDuration();
      });
      
      // Evento de checkbox de acesso central
      document.getElementById('hasCentralAccess').addEventListener('change', function() {
        const centralAccessSection = document.getElementById('centralAccessSection');
        centralAccessSection.classList.toggle('hidden', !this.checked);
        
        // Se o checkbox for marcado, atualizar o cálculo de tempo
        if (this.checked) {
          updateCatheterDuration();
        }
      });
      
      // Evento de mudança de data de inserção do cateter central
      document.getElementById('centralAccessInsertionDate').addEventListener('change', function() {
        updateCatheterDuration();
      });
      
      // Evento de checkbox de sedação
      document.getElementById('isUnderSedation').addEventListener('change', function() {
        const sedationSection = document.getElementById('sedationSection');
        sedationSection.classList.toggle('hidden', !this.checked);
      });
      
      // Adicionar sedação
      document.getElementById('addSedationBtn').addEventListener('click', function() {
        addSedation();
      });
      
      // Evento de checkbox de analgesia
      document.getElementById('isUnderAnalgesia').addEventListener('change', function() {
        const analgesiaSection = document.getElementById('analgesiaSection');
        analgesiaSection.classList.toggle('hidden', !this.checked);
      });
      
      // Adicionar analgésico
      document.getElementById('addAnalgesiaBtn').addEventListener('click', function() {
        addAnalgesia();
      });
      
      // Evento de checkbox de drogas vasoativas
      document.getElementById('isUnderVasopressors').addEventListener('change', function() {
        const vasopressorSection = document.getElementById('vasopressorSection');
        vasopressorSection.classList.toggle('hidden', !this.checked);
      });
      
      // Adicionar droga vasoativa
      document.getElementById('addVasopressorBtn').addEventListener('click', function() {
        addVasopressor();
      });
      
      // Evento de cancelamento de registro
      document.getElementById('cancelRecordBtn').addEventListener('click', function() {
        document.getElementById('dailyRecordForm').classList.add('hidden');
        document.getElementById('newRecordButtonContainer').style.display = 'block';
        manualTabSwitch('patientDetails');
      });
      
      // Painel nível de dor
      const painLevel = document.getElementById('painLevel');
      const painLevelValue = document.getElementById('painLevelValue');
      
      painLevel.addEventListener('input', function() {
        const value = this.value;
        let description = '';
        
        switch (parseInt(value)) {
          case 0:
            description = '0 - Sem dor';
            break;
          case 1:
          case 2:
            description = `${value} - Dor leve`;
            break;
          case 3:
          case 4:
            description = `${value} - Dor moderada`;
            break;
          case 5:
          case 6:
            description = `${value} - Dor considerável`;
            break;
          case 7:
          case 8:
            description = `${value} - Dor intensa`;
            break;
          case 9:
          case 10:
            description = `${value} - Dor extrema`;
            break;
        }
        
        painLevelValue.textContent = description;
      });
      
      // Adicionar medicamento
      document.getElementById('addMedicationBtn').addEventListener('click', addMedication);
      
      // Outros eventos...
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
    
    // Função para calcular e atualizar o tempo de uso do cateter central
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
    
    // Salvar registro diário
    function saveRecord(event) {
      event.preventDefault();
      logDebug('Salvando registro diário...');
      
      if (!validateRecordForm()) {
        showToast('Por favor, preencha todos os campos obrigatórios.', 'error');
        return;
      }
      
      // Coletar dados dos medicamentos
      const medicationEntries = document.querySelectorAll('.medication-entry');
      const medications = [];
      
      medicationEntries.forEach(entry => {
        const name = entry.querySelector('.medication-name').value.trim();
        const dose = entry.querySelector('.medication-dose').value.trim();
        const startDate = entry.querySelector('.medication-start-date')?.value || '';
        const route = entry.querySelector('.medication-route').value;
        
        if (name && dose) {
          medications.push({
            name,
            dose,
            startDate,
            route: route || 'Não especificada'
          });
        }
      });
      
      // Coletar dados de sedação, analgesia e drogas vasoativas (código não mostrado para brevidade)
      
      // Dados de acesso central
      const centralAccess = document.getElementById('hasCentralAccess').checked ? {
        location: document.getElementById('centralAccessLocation').value,
        insertionDate: document.getElementById('centralAccessInsertionDate').value,
        notes: document.getElementById('centralAccessNotes').value || ''
      } : null;
      
      const record = {
        id: appData.editingRecordId || generateId(),
        patientId: appData.selectedPatientId,
        date: document.getElementById('recordDate').value,
        time: document.getElementById('recordTime').value,
        vitalSigns: {
          temperature: document.getElementById('temperature').value || null,
          heartRate: document.getElementById('heartRate').value || null,
          bloodPressure: document.getElementById('bloodPressure').value || null,
          respiratoryRate: document.getElementById('respiratoryRate').value || null,
          oxygenSaturation: document.getElementById('oxygenSaturation').value || null,
          painLevel: document.getElementById('painLevel').value || null
        },
        medications: medications,
        procedures: document.getElementById('procedures').value,
        observations: document.getElementById('observations').value,
        nutritionalStatus: document.getElementById('nutritionalStatus').value,
        mobilityStatus: document.getElementById('mobilityStatus').value,
        intubation: document.getElementById('isIntubated').checked ? {
          startDate: document.getElementById('intubationStartDate').value,
          canBeExtubated: document.querySelector('input[name="canBeExtubated"]:checked')?.value || null,
          notes: document.getElementById('intubationNotes').value || '',
          ventilationParams: {
            mode: document.getElementById('ventilationMode').value || null,
            fio2: document.getElementById('fio2').value || null,
            vc: document.getElementById('vc').value || null,
            vt: document.getElementById('vt').value || null,
            respiratoryFrequency: document.getElementById('ventilatoryFrequency').value || null,
            peep: document.getElementById('peep').value || null,
            inspiratoryPressure: document.getElementById('inspiratoryPressure').value || null,
            peakPressure: document.getElementById('peakPressure').value || null,
            plateauPressure: document.getElementById('plateauPressure').value || null
          }
        } : null,
        centralAccess: centralAccess,
        // Outras propriedades como sedação, analgesia, etc.
        discharge: null
      };
      
      // Se for alta, adicionar informações de alta
      if (document.getElementById('dischargePatient').checked) {
        record.discharge = {
          reason: document.getElementById('dischargeReason').value,
          summary: document.getElementById('dischargeSummary').value,
          followUp: document.getElementById('followUpInstructions').value
        };
        
        // Atualizar paciente com data de alta
        const patient = appData.patients.find(p => p.id === appData.selectedPatientId);
        if (patient) {
          patient.dischargeDate = record.date;
          patient.isActive = false;
          logDebug('Paciente recebeu alta:', patient);
        }
      }
      
      // Adicionar ou atualizar o registro
      if (appData.editingRecordId) {
        const index = appData.records.findIndex(r => r.id === appData.editingRecordId);
        if (index !== -1) {
          appData.records[index] = record;
          showToast('Registro atualizado com sucesso.', 'success');
        }
      } else {
        appData.records.push(record);
        showToast('Registro adicionado com sucesso.', 'success');
      }
      
      // Salvar dados
      saveDataToStorage();
      
      // Limpar formulário
      document.getElementById('dailyRecordForm').classList.add('hidden');
      document.getElementById('newRecordButtonContainer').style.display = 'block';
      
      // Atualizar detalhes e histórico
      renderPatientDetails(appData.selectedPatientId);
      renderHistoryTimeline(appData.selectedPatientId);
      renderStats(appData.selectedPatientId);
      
      // Trocar para a aba de histórico
      manualTabSwitch('patientHistory');
    }
    
    // Função de visualização de registro
    function viewRecord(recordId) {
      logDebug('Visualizando registro:', recordId);
      
      const record = appData.records.find(r => r.id === recordId);
      if (!record) {
        showToast('Registro não encontrado', 'error');
        return;
      }
      
      const patient = appData.patients.find(p => p.id === record.patientId);
      const patientName = patient ? patient.name : 'Paciente desconhecido';
      
      // Verificar presença de informações específicas
      const hasIntubation = record.intubation !== null;
      const hasCentralAccess = record.centralAccess !== null;
      
      // Criar HTML para intubação
      let intubationHtml = '';
      if (hasIntubation) {
        let intubationTimeInfo = '';
        if (record.intubation.startDate) {
          const startDate = formatDate(record.intubation.startDate);
          const recordDate = new Date(record.date);
          const intubStartDate = new Date(record.intubation.startDate);
          const daysIntubated = Math.floor((recordDate - intubStartDate) / (1000 * 60 * 60 * 24));
          
          intubationTimeInfo = `
            <p><strong>Data de Início:</strong> ${startDate}</p>
            <p><strong>Tempo de Intubação:</strong> ${daysIntubated} dias</p>
          `;
        }
        
        // Criar HTML para parâmetros de ventilação
        let ventilationParamsHtml = '';
        if (record.intubation.ventilationParams) {
          const params = record.intubation.ventilationParams;
          let paramsList = '';
          
          if (params.mode) paramsList += `<li><strong>Modo:</strong> ${params.mode}</li>`;
          if (params.fio2) paramsList += `<li><strong>FiO2:</strong> ${params.fio2}%</li>`;
          if (params.vc) paramsList += `<li><strong>VC:</strong> ${params.vc} ml</li>`;
          if (params.vt) paramsList += `<li><strong>VT:</strong> ${params.vt} L/min</li>`;
          if (params.respiratoryFrequency) paramsList += `<li><strong>FR:</strong> ${params.respiratoryFrequency} irpm</li>`;
          if (params.peep) paramsList += `<li><strong>PEEP:</strong> ${params.peep} cmH₂O</li>`;
          if (params.inspiratoryPressure) paramsList += `<li><strong>Pressão Inspiratória:</strong> ${params.inspiratoryPressure} cmH₂O</li>`;
          if (params.peakPressure) paramsList += `<li><strong>Pressão de Pico:</strong> ${params.peakPressure} cmH₂O</li>`;
          if (params.plateauPressure) paramsList += `<li><strong>Pressão de Platô:</strong> ${params.plateauPressure} cmH₂O</li>`;
          
          if (paramsList) {
            ventilationParamsHtml = `
              <div class="card" style="padding: 0.75rem; margin: 0.5rem 0; background-color: rgba(93, 92, 222, 0.05);">
                <h5>Parâmetros de Ventilação Mecânica</h5>
                <ul>${paramsList}</ul>
              </div>
            `;
          }
        }
        
        intubationHtml = `
          <div class="divider"></div>
          <div class="record-intubation">
            <h4>Informações de Intubação</h4>
            ${intubationTimeInfo}
            <p><strong>Pode ser extubado?</strong> ${record.intubation.canBeExtubated === 'S' ? 'Sim' : record.intubation.canBeExtubated === 'N' ? 'Não' : 'Não informado'}</p>
            ${ventilationParamsHtml}
            ${record.intubation.notes ? `<p><strong>Observações sobre intubação:</strong> ${record.intubation.notes}</p>` : ''}
          </div>
        `;
      }
      
      // Criar HTML para acesso central
      let centralAccessHtml = '';
      if (hasCentralAccess) {
        const location = record.centralAccess.location;
        const insertionDate = formatDate(record.centralAccess.insertionDate);
        const notes = record.centralAccess.notes || '';
        
        // Calcular o tempo de uso até a data do registro
        let daysOfUseHtml = '';
        if (record.centralAccess.insertionDate) {
          const recordDate = new Date(record.date);
          const insertDate = new Date(record.centralAccess.insertionDate);
          const daysOfUse = Math.floor((recordDate - insertDate) / (1000 * 60 * 60 * 24));
          
          let daysClass = '';
          if (daysOfUse < 7) daysClass = 'text-success';
          else if (daysOfUse < 14) daysClass = 'text-warning';
          else daysClass = 'text-danger';
          
          daysOfUseHtml = `<p><strong>Tempo de Uso:</strong> <span class="${daysClass}">${daysOfUse} dias</span></p>`;
        }
        
        centralAccessHtml = `
          <div class="divider"></div>
          <div class="record-central-access">
            <h4>Acesso Central</h4>
            <p><strong>Localização:</strong> ${location}</p>
            <p><strong>Data de Inserção:</strong> ${insertionDate}</p>
            ${daysOfUseHtml}
            ${notes ? `<p><strong>Observações:</strong> ${notes}</p>` : ''}
          </div>
        `;
      }
      
      // Montar o HTML completo do registro
      const recordDetails = document.getElementById('recordDetails');
      recordDetails.innerHTML = `
        <div class="record-patient-info">
          <h3>${patientName}</h3>
          <p>Data/Hora: ${formatDateTime(record.date, record.time)}</p>
        </div>
        
        <div class="divider"></div>
        
        <div class="record-vital-signs">
          <h4>Sinais Vitais</h4>
          <!-- Detalhes dos sinais vitais -->
        </div>
        
        <!-- Outras seções como medicamentos, procedimentos, etc. -->
        
        ${intubationHtml}
        
        ${centralAccessHtml}
        
        <!-- Outras seções como sedação, alta, etc. -->
      `;
      
      showModal('viewRecordModal');
    }
    
    // Resto do código JavaScript...
  </script>
</body>
</html>
