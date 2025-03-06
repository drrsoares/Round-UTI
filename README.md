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
      opacity: 0;
      visibility: hidden;
      transition: opacity 0.3s ease, visibility 0.3s ease;
    }
    
    .modal-overlay.active {
      opacity: 1;
      visibility: visible;
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
      transform: scale(0.9);
      transition: transform 0.3s ease;
    }
    
    .modal-overlay.active .modal-content {
      transform: scale(1);
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
      display: flex;
      align-items: center;
      justify-content: center;
      width: 30px;
      height: 30px;
      border-radius: 50%;
      transition: background-color 0.2s ease;
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
    
    /* Skeleton loading */
    .skeleton {
      background: linear-gradient(90deg, var(--input-bg) 25%, var(--hover-bg) 50%, var(--input-bg) 75%);
      background-size: 200% 100%;
      animation: skeleton-loading 1.5s infinite;
      border-radius: 4px;
      height: 1rem;
      margin-bottom: 0.5rem;
    }
    
    @keyframes skeleton-loading {
      0% {
        background-position: 200% 0;
      }
      100% {
        background-position: -200% 0;
      }
    }
    
    .skeleton.title {
      height: 1.5rem;
      width: 70%;
      margin-bottom: 1rem;
    }
    
    .skeleton.text {
      height: 1rem;
      margin-bottom: 0.5rem;
    }
    
    .skeleton.text.short {
      width: 40%;
    }
    
    .skeleton.text.medium {
      width: 60%;
    }
    
    .skeleton.text.long {
      width: 80%;
    }
    
    .skeleton.button {
      height: 2.5rem;
      width: 100px;
      margin-bottom: 0.5rem;
    }
    
    /* Search bar */
    .search-container {
      position: relative;
      margin-bottom: 1rem;
    }
    
    .search-container input {
      padding-left: 2.5rem;
    }
    
    .search-icon {
      position: absolute;
      left: 0.75rem;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-color);
      opacity: 0.5;
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
    
    /* Melhorias para campos inválidos */
    .form-control.invalid {
      background-color: rgba(220, 53, 69, 0.05);
    }
    
    /* Exportação */
    .export-options {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      margin-bottom: 1rem;
    }
    
    /* Select aprimorado */
    select.form-control {
      appearance: none;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%23333' d='M6 8.825c-.2 0-.4-.1-.5-.2l-3.5-3.5c-.3-.3-.3-.8 0-1.1.3-.3.8-.3 1.1 0l2.9 2.9 2.9-2.9c.3-.3.8-.3 1.1 0 .3.3.3.8 0 1.1l-3.5 3.5c-.1.1-.3.2-.5.2z'/%3E%3C/svg%3E");
      background-repeat: no-repeat;
      background-position: right 0.75rem center;
      padding-right: 2rem;
    }
    
    @media (prefers-color-scheme: dark) {
      select.form-control {
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%23f0f0f0' d='M6 8.825c-.2 0-.4-.1-.5-.2l-3.5-3.5c-.3-.3-.3-.8 0-1.1.3-.3.8-.3 1.1 0l2.9 2.9 2.9-2.9c.3-.3.8-.3 1.1 0 .3.3.3.8 0 1.1l-3.5 3.5c-.1.1-.3.2-.5.2z'/%3E%3C/svg%3E");
      }
    }
    
    /* Tooltips */
    .tooltip {
      position: relative;
      display: inline-block;
      cursor: help;
    }
    
    .tooltip .tooltip-text {
      visibility: hidden;
      width: 200px;
      background-color: #555;
      color: #fff;
      text-align: center;
      border-radius: 6px;
      padding: 0.5rem;
      position: absolute;
      z-index: 1;
      bottom: 125%;
      left: 50%;
      margin-left: -100px;
      opacity: 0;
      transition: opacity 0.3s;
      font-size: 0.8rem;
    }
    
    .tooltip .tooltip-text::after {
      content: "";
      position: absolute;
      top: 100%;
      left: 50%;
      margin-left: -5px;
      border-width: 5px;
      border-style: solid;
      border-color: #555 transparent transparent transparent;
    }
    
    .tooltip:hover .tooltip-text {
      visibility: visible;
      opacity: 1;
    }
    
    /* Campo de observações */
    .notes-field {
      min-height: 100px;
      resize: vertical;
    }
    
    /* Responsividade aprimorada para dispositivos móveis */
    @media (max-width: 480px) {
      .form-group {
        margin-bottom: 0.75rem;
      }
      
      .form-control {
        padding: 0.5rem;
      }
      
      .btn {
        font-size: 0.9rem;
        padding: 0.4rem 0.8rem;
      }
      
      .card {
        padding: 0.75rem;
        margin-bottom: 1rem;
      }
      
      .tabs {
        justify-content: space-between;
      }
      
      .tab {
        padding: 0.5rem 0.75rem;
        font-size: 0.9rem;
        flex: 1;
        text-align: center;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="page-header">
      <h1>Sistema de Acompanhamento de Pacientes</h1>
      <div class="btn-group">
        <button id="newPatientBtn" class="btn btn-primary">
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
        <div class="tab active" data-tab="patientList">Lista de Pacientes</div>
        <div class="tab" data-tab="patientDetails">Detalhes do Paciente</div>
        <div class="tab" data-tab="dailyRecord">Registro Diário</div>
        <div class="tab" data-tab="patientHistory">Histórico</div>
        <div class="tab" data-tab="patientStats">Estatísticas</div>
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
          <div class="empty-state" id="emptyPatientList">
            <i class="fas fa-user-injured"></i>
            <div class="empty-state-text">Nenhum paciente cadastrado</div>
            <button class="btn btn-primary" id="emptyStateNewPatient">
              <i class="fas fa-user-plus"></i> Adicionar paciente
            </button>
          </div>
        </div>
      </div>
      
      <div id="patientDetails" class="tab-content">
        <div id="selectedPatientInfo">
          <!-- Detalhes do paciente serão carregados aqui -->
          <div class="empty-state">
            <i class="fas fa-user"></i>
            <div class="empty-state-text">Selecione um paciente para visualizar os detalhes</div>
          </div>
        </div>
        
        <div id="patientActions" class="btn-group hidden">
          <button id="editPatientBtn" class="btn btn-info">
            <i class="fas fa-edit"></i> Editar
          </button>
          <button id="newDailyRecordBtn" class="btn btn-primary">
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
        <div id="dailyRecordForm" class="hidden">
          <h2>Novo Registro Diário</h2>
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
              <label for="vitalSigns" class="form-label required-field">Sinais Vitais</label>
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
              <label for="medications" class="form-label">Medicamentos Administrados</label>
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
              <button type="button" id="addMedicationBtn" class="btn btn-sm btn-secondary mt-2">
                <i class="fas fa-plus"></i> Adicionar Medicamento
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
        
        <div id="dailyRecordEmptyState" class="empty-state">
          <i class="fas fa-clipboard-list"></i>
          <div class="empty-state-text">Selecione um paciente e crie um novo registro diário</div>
        </div>
      </div>
      
      <div id="patientHistory" class="tab-content">
        <div id="historyContainer" class="hidden">
          <div class="history-filters">
            <div class="flex-container">
              <div>
                <div class="form-group">
                  <label for="historyDateStart" class="form-label">Data inicial</label>
                  <input type="date" id="historyDateStart" class="form-control">
                </div>
              </div>
              <div>
                <div class="form-group">
                  <label for="historyDateEnd" class="form-label">Data final</label>
                  <input type="date" id="historyDateEnd" class="form-control">
                </div>
              </div>
              <div>
                <div class="form-group">
                  <label for="historyView" class="form-label">Visualização</label>
                  <select id="historyView" class="form-control">
                    <option value="timeline">Linha do tempo</option>
                    <option value="table">Tabela</option>
                  </select>
                </div>
              </div>
            </div>
            <button id="exportPatientBtn" class="btn btn-success">
              <i class="fas fa-file-export"></i> Exportar para Excel
            </button>
          </div>
          
          <div id="historyTimeline" class="history-timeline">
            <!-- Timeline de registros será carregada aqui -->
          </div>
          
          <div id="historyTable" class="table-container hidden">
            <table>
              <thead>
                <tr>
                  <th>Data/Hora</th>
                  <th>Sinais Vitais</th>
                  <th>Medicamentos</th>
                  <th>Observações</th>
                  <th>Ações</th>
                </tr>
              </thead>
              <tbody id="historyTableBody">
                <!-- Dados da tabela serão carregados aqui -->
              </tbody>
            </table>
          </div>
        </div>
        
        <div id="historyEmptyState" class="empty-state">
          <i class="fas fa-history"></i>
          <div class="empty-state-text">Selecione um paciente para visualizar o histórico</div>
        </div>
      </div>
      
      <div id="patientStats" class="tab-content">
        <div id="statsContainer" class="hidden">
          <div class="flex-container">
            <div class="card">
              <h3>Internação</h3>
              <div class="info-group">
                <p><strong>Data de Internação:</strong> <span id="statAdmissionDate">--/--/----</span></p>
                <p><strong>Diagnóstico:</strong> <span id="statDiagnosis">--</span></p>
                <p><strong>Tempo de Internação:</strong> <span id="statHospitalDays">--</span></p>
              </div>
            </div>
            <div class="card">
              <h3>Status Atual</h3>
              <div class="info-group">
                <p><strong>Situação:</strong> <span id="statCurrentStatus">--</span></p>
                <p><strong>Última Atualização:</strong> <span id="statLastUpdate">--/--/----</span></p>
              </div>
            </div>
          </div>
          
          <div class="card">
            <h3>Gráficos de Sinais Vitais</h3>
            <div class="form-group">
              <label for="vitalSignSelect" class="form-label">Selecione o sinal vital:</label>
              <select id="vitalSignSelect" class="form-control">
                <option value="temperature">Temperatura</option>
                <option value="heartRate">Frequência Cardíaca</option>
                <option value="oxygenSaturation">Saturação de O₂</option>
                <option value="painLevel">Nível de Dor</option>
              </select>
            </div>
            <div class="chart-container">
              <canvas id="vitalSignsChart"></canvas>
            </div>
          </div>
          
          <div class="card">
            <h3>Medicamentos Utilizados</h3>
            <div class="table-container">
              <table>
                <thead>
                  <tr>
                    <th>Medicamento</th>
                    <th>Dosagem</th>
                    <th>Via</th>
                    <th>Frequência</th>
                  </tr>
                </thead>
                <tbody id="medicationStatsTable">
                  <!-- Estatísticas de medicamentos serão carregadas aqui -->
                </tbody>
              </table>
            </div>
          </div>
        </div>
        
        <div id="statsEmptyState" class="empty-state">
          <i class="fas fa-chart-bar"></i>
          <div class="empty-state-text">Selecione um paciente para visualizar as estatísticas</div>
        </div>
      </div>
    </div>
    
    <!-- Modal de Novo/Editar Paciente -->
    <div id="patientModal" class="modal-overlay">
      <div class="modal-content">
        <button class="modal-close" id="closePatientModal"><i class="fas fa-times"></i></button>
        <h2 id="patientModalTitle">Novo Paciente</h2>
        <form id="patientForm">
          <div class="form-group">
            <label for="patientName" class="form-label required-field">Nome Completo</label>
            <input type="text" id="patientName" class="form-control" required>
            <div class="validation-message">Nome é obrigatório</div>
          </div>
          
          <div class="flex-container">
            <div>
              <div class="form-group">
                <label for="patientBirthdate" class="form-label required-field">Data de Nascimento</label>
                <input type="date" id="patientBirthdate" class="form-control" required>
                <div class="validation-message">Data de nascimento é obrigatória</div>
              </div>
            </div>
            <div>
              <div class="form-group">
                <label for="patientGender" class="form-label required-field">Gênero</label>
                <select id="patientGender" class="form-control" required>
                  <option value="">Selecione</option>
                  <option value="Masculino">Masculino</option>
                  <option value="Feminino">Feminino</option>
                  <option value="Outro">Outro</option>
                </select>
                <div class="validation-message">Gênero é obrigatório</div>
              </div>
            </div>
          </div>
          
          <div class="form-group">
            <label for="patientRecord" class="form-label required-field">Número de Registro</label>
            <input type="text" id="patientRecord" class="form-control" required>
            <div class="validation-message">Número de registro é obrigatório</div>
          </div>
          
          <div class="form-group">
            <label for="patientContact" class="form-label">Contato</label>
            <input type="tel" id="patientContact" class="form-control" placeholder="(00) 00000-0000">
          </div>
          
          <div class="form-group">
            <label for="patientAdmissionDate" class="form-label required-field">Data de Internação</label>
            <input type="date" id="patientAdmissionDate" class="form-control" required>
            <div class="validation-message">Data de internação é obrigatória</div>
          </div>
          
          <div class="form-group">
            <label for="patientDiagnosis" class="form-label required-field">Diagnóstico Principal</label>
            <textarea id="patientDiagnosis" class="form-control" required></textarea>
            <div class="validation-message">Diagnóstico é obrigatório</div>
          </div>
          
          <div class="form-group">
            <label for="patientAllergies" class="form-label">Alergias</label>
            <textarea id="patientAllergies" class="form-control" placeholder="Se não houver, deixe em branco"></textarea>
          </div>
          
          <div class="form-group">
            <label for="patientNotes" class="form-label">Observações Iniciais</label>
            <textarea id="patientNotes" class="form-control"></textarea>
          </div>
          
          <div class="btn-group">
            <button type="submit" id="savePatientBtn" class="btn btn-primary">
              <i class="fas fa-save"></i> Salvar
            </button>
            <button type="button" id="cancelPatientBtn" class="btn btn-secondary">
              <i class="fas fa-times"></i> Cancelar
            </button>
          </div>
        </form>
      </div>
    </div>
    
    <!-- Modal de Confirmação -->
    <div id="confirmModal" class="modal-overlay">
      <div class="modal-content">
        <button class="modal-close" id="closeConfirmModal"><i class="fas fa-times"></i></button>
        <h2>Confirmação</h2>
        <p id="confirmMessage">Tem certeza que deseja realizar esta ação?</p>
        <div class="btn-group">
          <button id="confirmYesBtn" class="btn btn-danger">Sim, confirmar</button>
          <button id="confirmNoBtn" class="btn btn-secondary">Cancelar</button>
        </div>
      </div>
    </div>
    
    <!-- Modal de Visualização do Registro -->
    <div id="viewRecordModal" class="modal-overlay">
      <div class="modal-content">
        <button class="modal-close" id="closeViewRecordModal"><i class="fas fa-times"></i></button>
        <h2>Detalhes do Registro</h2>
        <div id="recordDetails">
          <!-- Detalhes do registro serão carregados aqui -->
        </div>
        <div class="btn-group">
          <button id="closeViewRecordBtn" class="btn btn-secondary">Fechar</button>
        </div>
      </div>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="toast"></div>
  </div>

  <script>
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
      
      // Dados simulados para armazenamento (em substituição ao localStorage)
      let patients = [];
      let records = [];
      let selectedPatientId = null;
      let editingPatientId = null;
      let editingRecordId = null;
      
      // Elementos do DOM
      const tabs = document.querySelectorAll('.tab');
      const tabContents = document.querySelectorAll('.tab-content');
      const patientListContainer = document.getElementById('patientListContainer');
      const emptyPatientList = document.getElementById('emptyPatientList');
      const selectedPatientInfo = document.getElementById('selectedPatientInfo');
      const patientActions = document.getElementById('patientActions');
      const dailyRecordForm = document.getElementById('dailyRecordForm');
      const dailyRecordEmptyState = document.getElementById('dailyRecordEmptyState');
      const historyContainer = document.getElementById('historyContainer');
      const historyEmptyState = document.getElementById('historyEmptyState');
      const statsContainer = document.getElementById('statsContainer');
      const statsEmptyState = document.getElementById('statsEmptyState');
      const patientModal = document.getElementById('patientModal');
      const confirmModal = document.getElementById('confirmModal');
      const viewRecordModal = document.getElementById('viewRecordModal');
      const toast = document.getElementById('toast');
      const painLevel = document.getElementById('painLevel');
      const painLevelValue = document.getElementById('painLevelValue');
      const searchPatients = document.getElementById('searchPatients');
      const statusFilter = document.getElementById('statusFilter');
      const sortPatients = document.getElementById('sortPatients');
      const dischargePatient = document.getElementById('dischargePatient');
      const dischargeSection = document.getElementById('dischargeSection');
      
      // Buttons
      const newPatientBtn = document.getElementById('newPatientBtn');
      const emptyStateNewPatient = document.getElementById('emptyStateNewPatient');
      const editPatientBtn = document.getElementById('editPatientBtn');
      const newDailyRecordBtn = document.getElementById('newDailyRecordBtn');
      const dischargePatientBtn = document.getElementById('dischargePatientBtn');
      const deletePatientBtn = document.getElementById('deletePatientBtn');
      const addMedicationBtn = document.getElementById('addMedicationBtn');
      const saveRecordBtn = document.getElementById('saveRecordBtn');
      const cancelRecordBtn = document.getElementById('cancelRecordBtn');
      const savePatientBtn = document.getElementById('savePatientBtn');
      const cancelPatientBtn = document.getElementById('cancelPatientBtn');
      const closePatientModal = document.getElementById('closePatientModal');
      const closeConfirmModal = document.getElementById('closeConfirmModal');
      const confirmYesBtn = document.getElementById('confirmYesBtn');
      const confirmNoBtn = document.getElementById('confirmNoBtn');
      const closeViewRecordModal = document.getElementById('closeViewRecordModal');
      const closeViewRecordBtn = document.getElementById('closeViewRecordBtn');
      const exportAllBtn = document.getElementById('exportAllBtn');
      const exportPatientBtn = document.getElementById('exportPatientBtn');
      
      // Forms
      const patientForm = document.getElementById('patientForm');
      const recordForm = document.getElementById('recordForm');
      
      // Adicionar dados de exemplo
      function addSampleData() {
        if (patients.length === 0) {
          // Adicionar pacientes de exemplo
          const samplePatients = [
            {
              id: generateId(),
              name: 'João Silva',
              birthdate: '1965-05-10',
              gender: 'Masculino',
              record: '12345',
              contact: '(11) 98765-4321',
              admissionDate: '2023-06-15',
              diagnosis: 'Pneumonia comunitária',
              allergies: 'Penicilina',
              notes: 'Paciente com comorbidade de hipertensão e diabetes.',
              dischargeDate: null,
              isActive: true
            },
            {
              id: generateId(),
              name: 'Maria Oliveira',
              birthdate: '1978-11-22',
              gender: 'Feminino',
              record: '23456',
              contact: '(11) 91234-5678',
              admissionDate: '2023-06-20',
              diagnosis: 'Insuficiência cardíaca descompensada',
              allergies: 'Sulfas',
              notes: 'Paciente apresenta edema em membros inferiores.',
              dischargeDate: null,
              isActive: true
            }
          ];
          
          patients = samplePatients;
          
          // Adicionar registros de exemplo
          const sampleRecords = [
            {
              id: generateId(),
              patientId: patients[0].id,
              date: '2023-06-15',
              time: '14:30',
              vitalSigns: {
                temperature: 38.5,
                heartRate: 95,
                bloodPressure: '130/85',
                respiratoryRate: 20,
                oxygenSaturation: 93,
                painLevel: 3
              },
              medications: [
                {
                  name: 'Ceftriaxona',
                  dose: '1g',
                  route: 'Intravenosa'
                },
                {
                  name: 'Dipirona',
                  dose: '1g',
                  route: 'Oral'
                }
              ],
              procedures: 'Coleta de hemoculturas',
              observations: 'Paciente relata melhora da dispneia após medicação.',
              nutritionalStatus: 'Adequado',
              mobilityStatus: 'Deambula com auxílio',
              discharge: null
            },
            {
              id: generateId(),
              patientId: patients[0].id,
              date: '2023-06-16',
              time: '09:00',
              vitalSigns: {
                temperature: 37.2,
                heartRate: 88,
                bloodPressure: '125/80',
                respiratoryRate: 18,
                oxygenSaturation: 95,
                painLevel: 2
              },
              medications: [
                {
                  name: 'Ceftriaxona',
                  dose: '1g',
                  route: 'Intravenosa'
                }
              ],
              procedures: 'Raio-X de tórax',
              observations: 'Melhora dos sintomas respiratórios.',
              nutritionalStatus: 'Adequado',
              mobilityStatus: 'Deambula sem auxílio',
              discharge: null
            },
            {
              id: generateId(),
              patientId: patients[1].id,
              date: '2023-06-20',
              time: '10:15',
              vitalSigns: {
                temperature: 36.8,
                heartRate: 102,
                bloodPressure: '160/95',
                respiratoryRate: 22,
                oxygenSaturation: 91,
                painLevel: 4
              },
              medications: [
                {
                  name: 'Furosemida',
                  dose: '40mg',
                  route: 'Intravenosa'
                },
                {
                  name: 'Enalapril',
                  dose: '10mg',
                  route: 'Oral'
                }
              ],
              procedures: 'Aferição de peso e diurese',
              observations: 'Paciente com dispneia aos pequenos esforços e edema +2/+4 em MMII.',
              nutritionalStatus: 'Inapetente',
              mobilityStatus: 'Restrito ao leito',
              discharge: null
            }
          ];
          
          records = sampleRecords;
        }
      }
      
      addSampleData();
      
      // Funções de utilidade
      function generateId() {
        return Date.now().toString(36) + Math.random().toString(36).substr(2);
      }
      
      function formatDate(dateString) {
        if (!dateString) return '--';
        
        const date = new Date(dateString);
        return date.toLocaleDateString('pt-BR');
      }
      
      function formatDateTime(dateString, timeString) {
        if (!dateString) return '--';
        
        const date = new Date(dateString);
        const formattedDate = date.toLocaleDateString('pt-BR');
        
        if (timeString) {
          return `${formattedDate} ${timeString}`;
        }
        
        return formattedDate;
      }
      
      function calculateAge(birthdate) {
        const today = new Date();
        const birthDate = new Date(birthdate);
        let age = today.getFullYear() - birthDate.getFullYear();
        const monthDiff = today.getMonth() - birthDate.getMonth();
        
        if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
          age--;
        }
        
        return age;
      }
      
      function calculateHospitalDays(admissionDate, dischargeDate = null) {
        const start = new Date(admissionDate);
        const end = dischargeDate ? new Date(dischargeDate) : new Date();
        
        // Número de milissegundos em um dia
        const oneDay = 1000 * 60 * 60 * 24;
        
        // Diferença em milissegundos
        const diffTime = Math.abs(end - start);
        
        // Diferença em dias
        const diffDays = Math.floor(diffTime / oneDay);
        
        return diffDays;
      }
      
      function showToast(message, type = 'info') {
        toast.textContent = message;
        toast.className = 'toast';
        toast.classList.add(type);
        toast.classList.add('show');
        
        setTimeout(() => {
          toast.classList.remove('show');
        }, 3000);
      }
      
      function openModal(modal) {
        modal.classList.add('active');
      }
      
      function closeModal(modal) {
        modal.classList.remove('active');
      }
      
      function clearValidation(form) {
        const invalidInputs = form.querySelectorAll('.invalid');
        invalidInputs.forEach(input => {
          input.classList.remove('invalid');
        });
      }
      
      function validatePatientForm() {
        clearValidation(patientForm);
        let isValid = true;
        
        // Validar campos obrigatórios
        const requiredFields = [
          { field: 'patientName', message: 'Nome é obrigatório' },
          { field: 'patientBirthdate', message: 'Data de nascimento é obrigatória' },
          { field: 'patientGender', message: 'Gênero é obrigatório' },
          { field: 'patientRecord', message: 'Número de registro é obrigatório' },
          { field: 'patientAdmissionDate', message: 'Data de internação é obrigatória' },
          { field: 'patientDiagnosis', message: 'Diagnóstico é obrigatório' }
        ];
        
        requiredFields.forEach(({ field, message }) => {
          const input = document.getElementById(field);
          if (!input.value.trim()) {
            input.classList.add('invalid');
            input.nextElementSibling.textContent = message;
            isValid = false;
          }
        });
        
        return isValid;
      }
      
      function validateRecordForm() {
        clearValidation(recordForm);
        let isValid = true;
        
        // Validar campos obrigatórios
        const requiredFields = [
          { field: 'recordDate', message: 'Data é obrigatória' },
          { field: 'recordTime', message: 'Hora é obrigatória' }
        ];
        
        requiredFields.forEach(({ field, message }) => {
          const input = document.getElementById(field);
          if (!input.value.trim()) {
            input.classList.add('invalid');
            input.nextElementSibling.textContent = message;
            isValid = false;
          }
        });
        
        // Validar que pelo menos um sinal vital foi preenchido
        const vitalSigns = [
          document.getElementById('temperature'),
          document.getElementById('heartRate'),
          document.getElementById('bloodPressure'),
          document.getElementById('respiratoryRate'),
          document.getElementById('oxygenSaturation')
        ];
        
        const hasVitalSign = vitalSigns.some(input => input.value.trim() !== '');
        
        if (!hasVitalSign) {
          vitalSigns[0].parentElement.parentElement.parentElement.classList.add('invalid');
          document.querySelector('#vitalSigns + .validation-message').style.display = 'block';
          isValid = false;
        }
        
        // Validar campos de alta se checkbox estiver marcado
        if (dischargePatient.checked) {
          const dischargeRequiredFields = [
            { field: 'dischargeReason', message: 'Motivo da alta é obrigatório' },
            { field: 'dischargeSummary', message: 'Resumo da alta é obrigatório' }
          ];
          
          dischargeRequiredFields.forEach(({ field, message }) => {
            const input = document.getElementById(field);
            if (!input.value.trim()) {
              input.classList.add('invalid');
              input.nextElementSibling.textContent = message;
              isValid = false;
            }
          });
        }
        
        return isValid;
      }
      
      // Funções de renderização
      function renderPatientList() {
        if (patients.length === 0) {
          patientListContainer.innerHTML = '';
          emptyPatientList.classList.remove('hidden');
          return;
        }
        
        emptyPatientList.classList.add('hidden');
        
        let filteredPatients = [...patients];
        
        // Aplicar filtro de status
        if (statusFilter.value !== 'all') {
          const isActive = statusFilter.value === 'active';
          filteredPatients = filteredPatients.filter(patient => patient.isActive === isActive);
        }
        
        // Aplicar filtro de busca
        if (searchPatients.value.trim() !== '') {
          const searchTerm = searchPatients.value.trim().toLowerCase();
          filteredPatients = filteredPatients.filter(patient => 
            patient.name.toLowerCase().includes(searchTerm) || 
            patient.record.toLowerCase().includes(searchTerm) ||
            patient.diagnosis.toLowerCase().includes(searchTerm)
          );
        }
        
        // Aplicar ordenação
        switch (sortPatients.value) {
          case 'nameAsc':
            filteredPatients.sort((a, b) => a.name.localeCompare(b.name));
            break;
          case 'nameDesc':
            filteredPatients.sort((a, b) => b.name.localeCompare(a.name));
            break;
          case 'dateAsc':
            filteredPatients.sort((a, b) => new Date(a.admissionDate) - new Date(b.admissionDate));
            break;
          case 'dateDesc':
            filteredPatients.sort((a, b) => new Date(b.admissionDate) - new Date(a.admissionDate));
            break;
        }
        
        let html = '';
        
        filteredPatients.forEach(patient => {
          const isSelected = patient.id === selectedPatientId;
          const statusBadge = patient.isActive
            ? '<span class="badge badge-primary">Internado</span>'
            : '<span class="badge badge-success">Alta</span>';
          
          html += `
            <div class="patient-card ${isSelected ? 'selected' : ''}" data-id="${patient.id}">
              <div class="patient-info">
                <div class="patient-name">${patient.name} ${statusBadge}</div>
                <div class="patient-record">Registro: ${patient.record} | Internação: ${formatDate(patient.admissionDate)}</div>
              </div>
              <div class="patient-actions">
                <button class="btn btn-sm btn-info view-patient" data-id="${patient.id}">
                  <i class="fas fa-eye"></i>
                </button>
              </div>
            </div>
          `;
        });
        
        patientListContainer.innerHTML = html;
        
        // Adicionar eventos aos cards de pacientes
        const patientCards = document.querySelectorAll('.patient-card');
        patientCards.forEach(card => {
          card.addEventListener('click', function() {
            const patientId = this.dataset.id;
            selectPatient(patientId);
          });
        });
        
        const viewButtons = document.querySelectorAll('.view-patient');
        viewButtons.forEach(button => {
          button.addEventListener('click', function(e) {
            e.stopPropagation();
            const patientId = this.dataset.id;
            selectPatient(patientId);
            switchTab('patientDetails');
          });
        });
      }
      
      function renderPatientDetails(patientId) {
        const patient = patients.find(p => p.id === patientId);
        
        if (!patient) {
          selectedPatientInfo.innerHTML = `
            <div class="empty-state">
              <i class="fas fa-user"></i>
              <div class="empty-state-text">Selecione um paciente para visualizar os detalhes</div>
            </div>
          `;
          patientActions.classList.add('hidden');
          return;
        }
        
        const age = calculateAge(patient.birthdate);
        const hospitalDays = calculateHospitalDays(patient.admissionDate, patient.dischargeDate);
        
        const statusBadge = patient.isActive
          ? '<span class="badge badge-primary">Internado</span>'
          : `<span class="badge badge-success">Alta em ${formatDate(patient.dischargeDate)}</span>`;
        
        let html = `
          <div class="card">
            <h2>${patient.name} ${statusBadge}</h2>
            <div class="patient-basic-info">
              <p><strong>Registro:</strong> ${patient.record}</p>
              <p><strong>Idade:</strong> ${age} anos (${formatDate(patient.birthdate)})</p>
              <p><strong>Gênero:</strong> ${patient.gender}</p>
              <p><strong>Contato:</strong> ${patient.contact || 'Não informado'}</p>
            </div>
            
            <div class="divider"></div>
            
            <div class="patient-clinical-info">
              <p><strong>Data de Internação:</strong> ${formatDate(patient.admissionDate)}</p>
              <p><strong>Tempo de Internação:</strong> ${hospitalDays} dias</p>
              <p><strong>Diagnóstico:</strong> ${patient.diagnosis}</p>
              <p><strong>Alergias:</strong> ${patient.allergies || 'Nenhuma alergia conhecida'}</p>
            </div>
            
            <div class="divider"></div>
            
            <div class="patient-notes">
              <h3>Observações</h3>
              <p>${patient.notes || 'Sem observações adicionais'}</p>
            </div>
          </div>
        `;
        
        selectedPatientInfo.innerHTML = html;
        patientActions.classList.remove('hidden');
        
        // Desabilitar botão de alta se o paciente já teve alta
        if (!patient.isActive) {
          dischargePatientBtn.disabled = true;
          dischargePatientBtn.classList.add('opacity-50');
        } else {
          dischargePatientBtn.disabled = false;
          dischargePatientBtn.classList.remove('opacity-50');
        }
      }
      
      function renderHistoryTimeline(patientId) {
        const historyTimelineEl = document.getElementById('historyTimeline');
        const historyTableEl = document.getElementById('historyTable');
        const historyTableBodyEl = document.getElementById('historyTableBody');
        
        const patient = patients.find(p => p.id === patientId);
        if (!patient) return;
        
        const patientRecords = records.filter(r => r.patientId === patientId);
        
        if (patientRecords.length === 0) {
          historyTimelineEl.innerHTML = `
            <div class="empty-state">
              <i class="fas fa-clipboard-list"></i>
              <div class="empty-state-text">Nenhum registro disponível para este paciente</div>
            </div>
          `;
          historyTableBodyEl.innerHTML = '';
          return;
        }
        
        // Ordenar registros por data e hora
        patientRecords.sort((a, b) => {
          const dateA = new Date(`${a.date}T${a.time}`);
          const dateB = new Date(`${b.date}T${b.time}`);
          return dateB - dateA; // Do mais recente para o mais antigo
        });
        
        // Filtrar por data se os campos estiverem preenchidos
        const startDate = document.getElementById('historyDateStart').value;
        const endDate = document.getElementById('historyDateEnd').value;
        
        let filteredRecords = [...patientRecords];
        
        if (startDate) {
          filteredRecords = filteredRecords.filter(r => r.date >= startDate);
        }
        
        if (endDate) {
          filteredRecords = filteredRecords.filter(r => r.date <= endDate);
        }
        
        // Timeline
        let timelineHtml = '';
        
        filteredRecords.forEach(record => {
          const hasDischarge = record.discharge !== null;
          const dischargeBadge = hasDischarge ? '<span class="badge badge-success">Alta</span>' : '';
          
          const medications = record.medications.map(med => 
            `${med.name} ${med.dose} (${med.route})`
          ).join(', ');
          
          const vitals = [];
          if (record.vitalSigns.temperature) vitals.push(`Temp: ${record.vitalSigns.temperature}°C`);
          if (record.vitalSigns.heartRate) vitals.push(`FC: ${record.vitalSigns.heartRate} bpm`);
          if (record.vitalSigns.bloodPressure) vitals.push(`PA: ${record.vitalSigns.bloodPressure} mmHg`);
          if (record.vitalSigns.respiratoryRate) vitals.push(`FR: ${record.vitalSigns.respiratoryRate} irpm`);
          if (record.vitalSigns.oxygenSaturation) vitals.push(`SatO₂: ${record.vitalSigns.oxygenSaturation}%`);
          if (record.vitalSigns.painLevel) vitals.push(`Dor: ${record.vitalSigns.painLevel}/10`);
          
          timelineHtml += `
            <div class="history-item">
              <div class="history-date">
                ${formatDateTime(record.date, record.time)} ${dischargeBadge}
              </div>
              <div class="history-content">
                <p><strong>Sinais Vitais:</strong> ${vitals.join(' | ') || 'Não registrados'}</p>
                <p><strong>Medicamentos:</strong> ${medications || 'Nenhum medicamento registrado'}</p>
                ${record.procedures ? `<p><strong>Procedimentos:</strong> ${record.procedures}</p>` : ''}
                ${record.observations ? `<p><strong>Observações:</strong> ${record.observations}</p>` : ''}
                ${record.nutritionalStatus ? `<p><strong>Estado Nutricional:</strong> ${record.nutritionalStatus}</p>` : ''}
                ${record.mobilityStatus ? `<p><strong>Mobilidade:</strong> ${record.mobilityStatus}</p>` : ''}
                
                ${hasDischarge ? `
                  <div class="divider"></div>
                  <div class="discharge-info">
                    <p><strong>Motivo da Alta:</strong> ${record.discharge.reason}</p>
                    <p><strong>Resumo da Alta:</strong> ${record.discharge.summary}</p>
                    ${record.discharge.followUp ? `<p><strong>Instruções de Acompanhamento:</strong> ${record.discharge.followUp}</p>` : ''}
                  </div>
                ` : ''}
                
                <div class="text-right mt-2">
                  <button class="btn btn-sm btn-info view-record" data-id="${record.id}">
                    <i class="fas fa-eye"></i> Detalhes
                  </button>
                </div>
              </div>
            </div>
          `;
        });
        
        historyTimelineEl.innerHTML = timelineHtml;
        
        // Tabela
        let tableHtml = '';
        
        filteredRecords.forEach(record => {
          const hasDischarge = record.discharge !== null;
          const dischargeBadge = hasDischarge ? '<span class="badge badge-success">Alta</span>' : '';
          
          const medications = record.medications.map(med => 
            `${med.name} ${med.dose}`
          ).join(', ');
          
          const vitals = [];
          if (record.vitalSigns.temperature) vitals.push(`${record.vitalSigns.temperature}°C`);
          if (record.vitalSigns.heartRate) vitals.push(`FC: ${record.vitalSigns.heartRate}`);
          if (record.vitalSigns.oxygenSaturation) vitals.push(`SatO₂: ${record.vitalSigns.oxygenSaturation}%`);
          
          tableHtml += `
            <tr>
              <td>${formatDateTime(record.date, record.time)} ${dischargeBadge}</td>
              <td>${vitals.join(' | ') || '-'}</td>
              <td>${medications || '-'}</td>
              <td>${record.observations || '-'}</td>
              <td>
                <button class="btn btn-sm btn-info view-record" data-id="${record.id}">
                  <i class="fas fa-eye"></i> Ver
                </button>
              </td>
            </tr>
          `;
        });
        
        historyTableBodyEl.innerHTML = tableHtml;
        
        // Adicionar eventos aos botões de visualização de registro
        const viewRecordButtons = document.querySelectorAll('.view-record');
        viewRecordButtons.forEach(button => {
          button.addEventListener('click', function() {
            const recordId = this.dataset.id;
            viewRecord(recordId);
          });
        });
        
        // Mostrar visualização selecionada
        const historyView = document.getElementById('historyView').value;
        if (historyView === 'timeline') {
          historyTimelineEl.classList.remove('hidden');
          historyTableEl.classList.add('hidden');
        } else {
          historyTimelineEl.classList.add('hidden');
          historyTableEl.classList.remove('hidden');
        }
      }
      
      function renderStats(patientId) {
        const patient = patients.find(p => p.id === patientId);
        if (!patient) return;
        
        const patientRecords = records.filter(r => r.patientId === patientId);
        
        // Informações básicas
        document.getElementById('statAdmissionDate').textContent = formatDate(patient.admissionDate);
        document.getElementById('statDiagnosis').textContent = patient.diagnosis;
        document.getElementById('statHospitalDays').textContent = `${calculateHospitalDays(patient.admissionDate, patient.dischargeDate)} dias`;
        
        document.getElementById('statCurrentStatus').textContent = patient.isActive ? 'Internado' : 'Alta hospitalar';
        
        // Última atualização
        if (patientRecords.length > 0) {
          // Ordenar por data/hora decrescente
          patientRecords.sort((a, b) => {
            const dateA = new Date(`${a.date}T${a.time}`);
            const dateB = new Date(`${b.date}T${b.time}`);
            return dateB - dateA;
          });
          
          document.getElementById('statLastUpdate').textContent = formatDateTime(patientRecords[0].date, patientRecords[0].time);
        } else {
          document.getElementById('statLastUpdate').textContent = 'Nenhum registro';
        }
        
        // Renderizar gráfico
        renderVitalSignsChart(patientRecords);
        
        // Tabela de medicamentos utilizados
        const medicationStatsTable = document.getElementById('medicationStatsTable');
        
        // Calcular estatísticas de medicamentos
        const medications = {};
        
        patientRecords.forEach(record => {
          record.medications.forEach(med => {
            const key = `${med.name}-${med.dose}-${med.route}`;
            if (!medications[key]) {
              medications[key] = {
                name: med.name,
                dose: med.dose,
                route: med.route,
                count: 0
              };
            }
            medications[key].count++;
          });
        });
        
        // Ordenar medicamentos pelo número de vezes administrados
        const medicationList = Object.values(medications).sort((a, b) => b.count - a.count);
        
        let medicationHtml = '';
        
        medicationList.forEach(med => {
          medicationHtml += `
            <tr>
              <td>${med.name}</td>
              <td>${med.dose}</td>
              <td>${med.route}</td>
              <td>${med.count} vezes</td>
            </tr>
          `;
        });
        
        if (medicationList.length === 0) {
          medicationHtml = `
            <tr>
              <td colspan="4" class="text-center">Nenhum medicamento registrado</td>
            </tr>
          `;
        }
        
        medicationStatsTable.innerHTML = medicationHtml;
      }
      
      function renderVitalSignsChart(patientRecords) {
        const canvas = document.getElementById('vitalSignsChart');
        const vitalSignSelect = document.getElementById('vitalSignSelect');
        const selectedVital = vitalSignSelect.value;
        
        // Limpar o canvas
        if (window.vitalSignsChart) {
          window.vitalSignsChart.destroy();
        }
        
        if (patientRecords.length === 0) {
          return;
        }
        
        // Ordenar registros por data e hora
        patientRecords.sort((a, b) => {
          const dateA = new Date(`${a.date}T${a.time}`);
          const dateB = new Date(`${b.date}T${b.time}`);
          return dateA - dateB;
        });
        
        // Configurar dados para o gráfico
        const labels = patientRecords.map(record => formatDateTime(record.date, record.time));
        
        let chartLabel = '';
        let chartData = [];
        let borderColor = '';
        let yAxisConfig = {};
        
        switch (selectedVital) {
          case 'temperature':
            chartLabel = 'Temperatura (°C)';
            chartData = patientRecords.map(record => record.vitalSigns.temperature || null);
            borderColor = '#ff6384';
            yAxisConfig = {
              min: 35,
              max: 40,
              ticks: {
                stepSize: 0.5
              }
            };
            break;
          case 'heartRate':
            chartLabel = 'Frequência Cardíaca (bpm)';
            chartData = patientRecords.map(record => record.vitalSigns.heartRate || null);
            borderColor = '#36a2eb';
            yAxisConfig = {
              min: 40,
              max: 180,
              ticks: {
                stepSize: 20
              }
            };
            break;
          case 'oxygenSaturation':
            chartLabel = 'Saturação de O₂ (%)';
            chartData = patientRecords.map(record => record.vitalSigns.oxygenSaturation || null);
            borderColor = '#4bc0c0';
            yAxisConfig = {
              min: 70,
              max: 100,
              ticks: {
                stepSize: 5
              }
            };
            break;
          case 'painLevel':
            chartLabel = 'Nível de Dor (0-10)';
            chartData = patientRecords.map(record => record.vitalSigns.painLevel || null);
            borderColor = '#ff9f40';
            yAxisConfig = {
              min: 0,
              max: 10,
              ticks: {
                stepSize: 1
              }
            };
            break;
        }
        
        // Criar o gráfico
        window.vitalSignsChart = new Chart(canvas, {
          type: 'line',
          data: {
            labels: labels,
            datasets: [{
              label: chartLabel,
              data: chartData,
              borderColor: borderColor,
              backgroundColor: borderColor + '33',
              fill: true,
              tension: 0.1,
              pointBackgroundColor: borderColor,
              pointRadius: 4,
              pointHoverRadius: 6
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                position: 'top',
              },
              tooltip: {
                mode: 'index',
                intersect: false,
              }
            },
            scales: {
              y: yAxisConfig,
              x: {
                ticks: {
                  maxRotation: 45,
                  minRotation: 45
                }
              }
            }
          }
        });
      }
      
      // Exportação para Excel
      function exportToExcel(data, sheetName, fileName) {
        const worksheet = XLSX.utils.json_to_sheet(data);
        const workbook = XLSX.utils.book_new();
        XLSX.utils.book_append_sheet(workbook, worksheet, sheetName);
        
        // Gerar arquivo Excel
        XLSX.writeFile(workbook, fileName);
      }
      
      function preparePatientExport(patientId) {
        const patient = patients.find(p => p.id === patientId);
        if (!patient) return;
        
        const patientRecords = records.filter(r => r.patientId === patientId);
        
        const exportData = patientRecords.map(record => {
          // Transformar medicamentos em texto
          const medications = record.medications
            .map(med => `${med.name} ${med.dose} (${med.route})`)
            .join('; ');
          
          // Transformar sinais vitais em colunas separadas
          return {
            'Data': formatDate(record.date),
            'Hora': record.time,
            'Temperatura (°C)': record.vitalSigns.temperature || '',
            'Freq. Cardíaca (bpm)': record.vitalSigns.heartRate || '',
            'Pressão Arterial (mmHg)': record.vitalSigns.bloodPressure || '',
            'Freq. Respiratória (irpm)': record.vitalSigns.respiratoryRate || '',
            'Saturação O₂ (%)': record.vitalSigns.oxygenSaturation || '',
            'Nível de Dor (0-10)': record.vitalSigns.painLevel || '',
            'Medicamentos': medications,
            'Procedimentos': record.procedures || '',
            'Observações': record.observations || '',
            'Estado Nutricional': record.nutritionalStatus || '',
            'Mobilidade': record.mobilityStatus || '',
            'Alta': record.discharge ? 'Sim' : 'Não',
            'Motivo da Alta': record.discharge ? record.discharge.reason : '',
            'Resumo da Alta': record.discharge ? record.discharge.summary : ''
          };
        });
        
        const fileName = `Histórico_${patient.record}_${patient.name.replace(/ /g, '_')}.xlsx`;
        
        exportToExcel(exportData, 'Histórico do Paciente', fileName);
      }
      
      function prepareAllPatientsExport() {
        // Criar planilha de pacientes
        const patientsData = patients.map(patient => {
          return {
            'Registro': patient.record,
            'Nome': patient.name,
            'Data de Nascimento': formatDate(patient.birthdate),
            'Gênero': patient.gender,
            'Contato': patient.contact || '',
            'Data de Internação': formatDate(patient.admissionDate),
            'Data de Alta': patient.dischargeDate ? formatDate(patient.dischargeDate) : '',
            'Tempo de Internação (dias)': calculateHospitalDays(patient.admissionDate, patient.dischargeDate),
            'Diagnóstico': patient.diagnosis,
            'Alergias': patient.allergies || '',
            'Observações': patient.notes || '',
            'Status': patient.isActive ? 'Internado' : 'Alta'
          };
        });
        
        // Criar planilha de registros diários
        const recordsData = records.map(record => {
          const patient = patients.find(p => p.id === record.patientId);
          const patientName = patient ? patient.name : '';
          const patientRecord = patient ? patient.record : '';
          
          // Transformar medicamentos em texto
          const medications = record.medications
            .map(med => `${med.name} ${med.dose} (${med.route})`)
            .join('; ');
          
          return {
            'Registro do Paciente': patientRecord,
            'Nome do Paciente': patientName,
            'Data': formatDate(record.date),
            'Hora': record.time,
            'Temperatura (°C)': record.vitalSigns.temperature || '',
            'Freq. Cardíaca (bpm)': record.vitalSigns.heartRate || '',
            'Pressão Arterial (mmHg)': record.vitalSigns.bloodPressure || '',
            'Freq. Respiratória (irpm)': record.vitalSigns.respiratoryRate || '',
            'Saturação O₂ (%)': record.vitalSigns.oxygenSaturation || '',
            'Nível de Dor (0-10)': record.vitalSigns.painLevel || '',
            'Medicamentos': medications,
            'Procedimentos': record.procedures || '',
            'Observações': record.observations || '',
            'Estado Nutricional': record.nutritionalStatus || '',
            'Mobilidade': record.mobilityStatus || '',
            'Alta': record.discharge ? 'Sim' : 'Não',
            'Motivo da Alta': record.discharge ? record.discharge.reason : '',
            'Resumo da Alta': record.discharge ? record.discharge.summary : ''
          };
        });
        
        // Criar um arquivo Excel com múltiplas planilhas
        const workbook = XLSX.utils.book_new();
        
        // Adicionar planilha de pacientes
        const patientsWorksheet = XLSX.utils.json_to_sheet(patientsData);
        XLSX.utils.book_append_sheet(workbook, patientsWorksheet, 'Pacientes');
        
        // Adicionar planilha de registros
        const recordsWorksheet = XLSX.utils.json_to_sheet(recordsData);
        XLSX.utils.book_append_sheet(workbook, recordsWorksheet, 'Registros Diários');
        
        // Gerar arquivo Excel
        XLSX.writeFile(workbook, 'Sistema_Acompanhamento_Pacientes.xlsx');
      }
      
      // Manipulação de pacientes e registros
      function selectPatient(patientId) {
        selectedPatientId = patientId;
        
        // Atualizar visualização da lista
        const patientCards = document.querySelectorAll('.patient-card');
        patientCards.forEach(card => {
          if (card.dataset.id === patientId) {
            card.classList.add('selected');
          } else {
            card.classList.remove('selected');
          }
        });
        
        // Atualizar visualização de detalhes
        renderPatientDetails(patientId);
        
        // Atualizar histórico
        historyContainer.classList.remove('hidden');
        historyEmptyState.classList.add('hidden');
        renderHistoryTimeline(patientId);
        
        // Atualizar estatísticas
        statsContainer.classList.remove('hidden');
        statsEmptyState.classList.add('hidden');
        renderStats(patientId);
        
        // Habilitar botão de registro diário
        const patient = patients.find(p => p.id === patientId);
        if (patient && patient.isActive) {
          newDailyRecordBtn.classList.remove('opacity-50');
          newDailyRecordBtn.disabled = false;
        } else {
          newDailyRecordBtn.classList.add('opacity-50');
          newDailyRecordBtn.disabled = true;
        }
      }
      
      function newPatient() {
        editingPatientId = null;
        
        // Limpar formulário
        patientForm.reset();
        
        // Preencher a data de internação com a data atual
        document.getElementById('patientAdmissionDate').value = new Date().toISOString().slice(0, 10);
        
        // Limpar validação
        clearValidation(patientForm);
        
        // Atualizar título do modal
        document.getElementById('patientModalTitle').textContent = 'Novo Paciente';
        
        // Abrir modal
        openModal(patientModal);
      }
      
      function editPatient(patientId) {
        const patient = patients.find(p => p.id === patientId);
        if (!patient) return;
        
        editingPatientId = patientId;
        
        // Preencher formulário
        document.getElementById('patientName').value = patient.name;
        document.getElementById('patientBirthdate').value = patient.birthdate;
        document.getElementById('patientGender').value = patient.gender;
        document.getElementById('patientRecord').value = patient.record;
        document.getElementById('patientContact').value = patient.contact || '';
        document.getElementById('patientAdmissionDate').value = patient.admissionDate;
        document.getElementById('patientDiagnosis').value = patient.diagnosis;
        document.getElementById('patientAllergies').value = patient.allergies || '';
        document.getElementById('patientNotes').value = patient.notes || '';
        
        // Limpar validação
        clearValidation(patientForm);
        
        // Atualizar título do modal
        document.getElementById('patientModalTitle').textContent = 'Editar Paciente';
        
        // Abrir modal
        openModal(patientModal);
      }
      
      function savePatient(event) {
        event.preventDefault();
        
        if (!validatePatientForm()) {
          showToast('Por favor, preencha todos os campos obrigatórios.', 'error');
          return;
        }
        
        const patient = {
          id: editingPatientId || generateId(),
          name: document.getElementById('patientName').value,
          birthdate: document.getElementById('patientBirthdate').value,
          gender: document.getElementById('patientGender').value,
          record: document.getElementById('patientRecord').value,
          contact: document.getElementById('patientContact').value,
          admissionDate: document.getElementById('patientAdmissionDate').value,
          diagnosis: document.getElementById('patientDiagnosis').value,
          allergies: document.getElementById('patientAllergies').value,
          notes: document.getElementById('patientNotes').value,
          dischargeDate: null,
          isActive: true
        };
        
        if (editingPatientId) {
          // Atualizar paciente existente
          const index = patients.findIndex(p => p.id === editingPatientId);
          if (index !== -1) {
            // Preservar dados de alta se existirem
            if (patients[index].dischargeDate) {
              patient.dischargeDate = patients[index].dischargeDate;
              patient.isActive = patients[index].isActive;
            }
            
            patients[index] = patient;
            showToast('Paciente atualizado com sucesso.', 'success');
          }
        } else {
          // Adicionar novo paciente
          patients.push(patient);
          showToast('Paciente cadastrado com sucesso.', 'success');
        }
        
        // Fechar modal
        closeModal(patientModal);
        
        // Atualizar lista de pacientes
        renderPatientList();
        
        // Selecionar o paciente
        selectPatient(patient.id);
        
        // Trocar para a aba de detalhes
        switchTab('patientDetails');
      }
      
      function deletePatient(patientId) {
        const patient = patients.find(p => p.id === patientId);
        if (!patient) return;
        
        const patientRecords = records.filter(r => r.patientId === patientId);
        
        document.getElementById('confirmMessage').textContent = `Tem certeza que deseja excluir o paciente ${patient.name} e todos os seus ${patientRecords.length} registros?`;
        
        confirmYesBtn.onclick = function() {
          // Remover registros do paciente
          records = records.filter(r => r.patientId !== patientId);
          
          // Remover paciente
          patients = patients.filter(p => p.id !== patientId);
          
          // Fechar modal
          closeModal(confirmModal);
          
          // Atualizar lista de pacientes
          renderPatientList();
          
          // Limpar seleção
          selectedPatientId = null;
          renderPatientDetails(null);
          historyContainer.classList.add('hidden');
          historyEmptyState.classList.remove('hidden');
          statsContainer.classList.add('hidden');
          statsEmptyState.classList.remove('hidden');
          
          // Trocar para a aba de lista de pacientes
          switchTab('patientList');
          
          showToast('Paciente excluído com sucesso.', 'success');
        };
        
        // Abrir modal de confirmação
        openModal(confirmModal);
      }
      
      function dischargePatient(patientId) {
        const patient = patients.find(p => p.id === patientId);
        if (!patient || !patient.isActive) return;
        
        // Criar formulário de alta
        dailyRecordForm.classList.remove('hidden');
        dailyRecordEmptyState.classList.add('hidden');
        
        // Preencher data e hora atual
        const now = new Date();
        document.getElementById('recordDate').value = now.toISOString().slice(0, 10);
        document.getElementById('recordTime').value = now.toTimeString().slice(0, 5);
        
        // Ativar checkbox de alta
        dischargePatient.checked = true;
        dischargeSection.classList.remove('hidden');
        
        // Trocar para a aba de registro diário
        switchTab('dailyRecord');
        
        showToast('Preencha os dados da alta do paciente.', 'info');
      }
      
      function newDailyRecord() {
        editingRecordId = null;
        
        // Limpar formulário
        recordForm.reset();
        
        // Preencher data e hora atual
        const now = new Date();
        document.getElementById('recordDate').value = now.toISOString().slice(0, 10);
        document.getElementById('recordTime').value = now.toTimeString().slice(0, 5);
        
        // Esconder seção de alta
        dischargePatient.checked = false;
        dischargeSection.classList.add('hidden');
        
        // Limpar lista de medicamentos
        const medicationsList = document.getElementById('medicationsList');
        medicationsList.innerHTML = `
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
        `;
        
        // Mostrar formulário
        dailyRecordForm.classList.remove('hidden');
        dailyRecordEmptyState.classList.add('hidden');
        
        // Limpar validação
        clearValidation(recordForm);
        
        // Trocar para a aba de registro diário
        switchTab('dailyRecord');
      }
      
      function saveRecord(event) {
        event.preventDefault();
        
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
          const route = entry.querySelector('.medication-route').value;
          
          if (name && dose) {
            medications.push({
              name,
              dose,
              route: route || 'Não especificada'
            });
          }
        });
        
        const record = {
          id: editingRecordId || generateId(),
          patientId: selectedPatientId,
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
          discharge: null
        };
        
        // Se for alta, adicionar informações de alta
        if (dischargePatient.checked) {
          record.discharge = {
            reason: document.getElementById('dischargeReason').value,
            summary: document.getElementById('dischargeSummary').value,
            followUp: document.getElementById('followUpInstructions').value
          };
          
          // Atualizar paciente com data de alta
          const patient = patients.find(p => p.id === selectedPatientId);
          if (patient) {
            patient.dischargeDate = record.date;
            patient.isActive = false;
          }
        }
        
        if (editingRecordId) {
          // Atualizar registro existente
          const index = records.findIndex(r => r.id === editingRecordId);
          if (index !== -1) {
            records[index] = record;
            showToast('Registro atualizado com sucesso.', 'success');
          }
        } else {
          // Adicionar novo registro
          records.push(record);
          showToast('Registro adicionado com sucesso.', 'success');
        }
        
        // Limpar formulário
        dailyRecordForm.classList.add('hidden');
        dailyRecordEmptyState.classList.remove('hidden');
        
        // Atualizar histórico
        renderHistoryTimeline(selectedPatientId);
        
        // Atualizar detalhes do paciente
        renderPatientDetails(selectedPatientId);
        
        // Atualizar estatísticas
        renderStats(selectedPatientId);
        
        // Trocar para a aba de histórico
        switchTab('patientHistory');
      }
      
      function viewRecord(recordId) {
        const record = records.find(r => r.id === recordId);
        if (!record) return;
        
        const patient = patients.find(p => p.id === record.patientId);
        const patientName = patient ? patient.name : 'Paciente desconhecido';
        
        const medications = record.medications.map(med => 
          `<li>${med.name} ${med.dose} (${med.route})</li>`
        ).join('');
        
        const vitals = [];
        if (record.vitalSigns.temperature) vitals.push(`<li>Temperatura: ${record.vitalSigns.temperature}°C</li>`);
        if (record.vitalSigns.heartRate) vitals.push(`<li>Freq. Cardíaca: ${record.vitalSigns.heartRate} bpm</li>`);
        if (record.vitalSigns.bloodPressure) vitals.push(`<li>Pressão Arterial: ${record.vitalSigns.bloodPressure} mmHg</li>`);
        if (record.vitalSigns.respiratoryRate) vitals.push(`<li>Freq. Respiratória: ${record.vitalSigns.respiratoryRate} irpm</li>`);
        if (record.vitalSigns.oxygenSaturation) vitals.push(`<li>Saturação O₂: ${record.vitalSigns.oxygenSaturation}%</li>`);
        if (record.vitalSigns.painLevel) vitals.push(`<li>Nível de Dor: ${record.vitalSigns.painLevel}/10</li>`);
        
        const hasDischarge = record.discharge !== null;
        
        const recordDetails = document.getElementById('recordDetails');
        recordDetails.innerHTML = `
          <div class="record-patient-info">
            <h3>${patientName}</h3>
            <p>Data/Hora: ${formatDateTime(record.date, record.time)}</p>
          </div>
          
          <div class="divider"></div>
          
          <div class="record-vital-signs">
            <h4>Sinais Vitais</h4>
            ${vitals.length > 0 ? `<ul>${vitals.join('')}</ul>` : '<p>Nenhum sinal vital registrado</p>'}
          </div>
          
          <div class="record-medications">
            <h4>Medicamentos</h4>
            ${medications.length > 0 ? `<ul>${medications}</ul>` : '<p>Nenhum medicamento registrado</p>'}
          </div>
          
          ${record.procedures ? `
            <div class="record-procedures">
              <h4>Procedimentos</h4>
              <p>${record.procedures}</p>
            </div>
          ` : ''}
          
          ${record.observations ? `
            <div class="record-observations">
              <h4>Observações</h4>
              <p>${record.observations}</p>
            </div>
          ` : ''}
          
          ${record.nutritionalStatus ? `
            <div class="record-nutrition">
              <h4>Estado Nutricional</h4>
              <p>${record.nutritionalStatus}</p>
            </div>
          ` : ''}
          
          ${record.mobilityStatus ? `
            <div class="record-mobility">
              <h4>Mobilidade</h4>
              <p>${record.mobilityStatus}</p>
            </div>
          ` : ''}
          
          ${hasDischarge ? `
            <div class="divider"></div>
            
            <div class="record-discharge">
              <h4>Informações de Alta</h4>
              <p><strong>Motivo da Alta:</strong> ${record.discharge.reason}</p>
              <p><strong>Resumo da Alta:</strong> ${record.discharge.summary}</p>
              ${record.discharge.followUp ? `<p><strong>Instruções de Acompanhamento:</strong> ${record.discharge.followUp}</p>` : ''}
            </div>
          ` : ''}
        `;
        
        openModal(viewRecordModal);
      }
      
      // Funções auxiliares
      function switchTab(tabId) {
        tabs.forEach(tab => {
          if (tab.dataset.tab === tabId) {
            tab.classList.add('active');
          } else {
            tab.classList.remove('active');
          }
        });
        
        tabContents.forEach(content => {
          if (content.id === tabId) {
            content.classList.add('active');
          } else {
            content.classList.remove('active');
          }
        });
      }
      
      function addMedication() {
        const medicationsList = document.getElementById('medicationsList');
        const newEntry = document.createElement('div');
        newEntry.className = 'medication-entry';
        newEntry.innerHTML = `
          <div class="flex-container">
            <div>
              <div class="form-group">
                <label for="medicationName" class="form-label">Nome</label>
                <input type="text" class="form-control medication-name">
              </div>
            </div>
            <div>
              <div class="form-group">
                <label for="medicationDose" class="form-label">Dose</label>
                <input type="text" class="form-control medication-dose">
              </div>
            </div>
          </div>
          <div class="form-group">
            <label for="medicationRoute" class="form-label">Via de Administração</label>
            <select class="form-control medication-route">
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
          <button type="button" class="btn btn-sm btn-danger remove-medication mt-2">
            <i class="fas fa-trash-alt"></i> Remover
          </button>
        `;
        
        medicationsList.appendChild(newEntry);
        
        // Adicionar evento ao botão de remover
        const removeButton = newEntry.querySelector('.remove-medication');
        removeButton.addEventListener('click', function() {
          medicationsList.removeChild(newEntry);
        });
      }
      
      // Eventos
      // Navegação por abas
      tabs.forEach(tab => {
        tab.addEventListener('click', function() {
          const tabId = this.dataset.tab;
          switchTab(tabId);
        });
      });
      
      // Eventos de pacientes
      newPatientBtn.addEventListener('click', newPatient);
      emptyStateNewPatient.addEventListener('click', newPatient);
      editPatientBtn.addEventListener('click', function() {
        editPatient(selectedPatientId);
      });
      deletePatientBtn.addEventListener('click', function() {
        deletePatient(selectedPatientId);
      });
      dischargePatientBtn.addEventListener('click', function() {
        dischargePatient(selectedPatientId);
      });
      patientForm.addEventListener('submit', savePatient);
      closePatientModal.addEventListener('click', function() {
        closeModal(patientModal);
      });
      cancelPatientBtn.addEventListener('click', function() {
        closeModal(patientModal);
      });
      
      // Eventos de registro diário
      newDailyRecordBtn.addEventListener('click', newDailyRecord);
      addMedicationBtn.addEventListener('click', addMedication);
      recordForm.addEventListener('submit', saveRecord);
      cancelRecordBtn.addEventListener('click', function() {
        dailyRecordForm.classList.add('hidden');
        dailyRecordEmptyState.classList.remove('hidden');
        switchTab('patientDetails');
      });
      
      // Eventos de modal de confirmação
      closeConfirmModal.addEventListener('click', function() {
        closeModal(confirmModal);
      });
      confirmNoBtn.addEventListener('click', function() {
        closeModal(confirmModal);
      });
      
      // Eventos de modal de visualização de registro
      closeViewRecordModal.addEventListener('click', function() {
        closeModal(viewRecordModal);
      });
      closeViewRecordBtn.addEventListener('click', function() {
        closeModal(viewRecordModal);
      });
      
      // Eventos de exportação
      exportAllBtn.addEventListener('click', function() {
        prepareAllPatientsExport();
        showToast('Exportação concluída com sucesso.', 'success');
      });
      
      exportPatientBtn.addEventListener('click', function() {
        if (selectedPatientId) {
          preparePatientExport(selectedPatientId);
          showToast('Exportação concluída com sucesso.', 'success');
        }
      });
      
      // Eventos de filtros e busca
      searchPatients.addEventListener('input', function() {
        renderPatientList();
      });
      
      statusFilter.addEventListener('change', function() {
        renderPatientList();
      });
      
      sortPatients.addEventListener('change', function() {
        renderPatientList();
      });
      
      // Eventos do histórico
      document.getElementById('historyDateStart').addEventListener('change', function() {
        renderHistoryTimeline(selectedPatientId);
      });
      
      document.getElementById('historyDateEnd').addEventListener('change', function() {
        renderHistoryTimeline(selectedPatientId);
      });
      
      document.getElementById('historyView').addEventListener('change', function() {
        renderHistoryTimeline(selectedPatientId);
      });
      
      // Eventos de estatísticas
      document.getElementById('vitalSignSelect').addEventListener('change', function() {
        renderVitalSignsChart(records.filter(r => r.patientId === selectedPatientId));
      });
      
      // Evento de nível de dor
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
      
      // Evento de checkbox de alta
      dischargePatient.addEventListener('change', function() {
        if (this.checked) {
          dischargeSection.classList.remove('hidden');
        } else {
          dischargeSection.classList.add('hidden');
        }
      });
      
      // Inicialização
      renderPatientList();
    });
  </script>
</body>
</html>
