# Round-UTI
Formulario para Round Diario na UTI
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAST HUG - Sistema Integrado de Avaliação</title>

    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
            line-height: 1.6;
        }

        .card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .form-group {
            margin-bottom: 15px;
            padding: 10px 0;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #333333;
        }

        input, 
        select, 
        textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #dddddd;
            border-radius: 4px;
            box-sizing: border-box;
            font-size: 14px;
        }

        textarea {
            resize: vertical;
            min-height: 60px;
        }

        .checkbox-group {
            margin: 8px 0;
            padding: 5px 0;
        }

        .checkbox-group input[type="radio"],
        .checkbox-group input[type="checkbox"] {
            width: auto;
            margin-right: 8px;
            cursor: pointer;
        }

        .checkbox-group label {
            display: inline;
            font-weight: normal;
            cursor: pointer;
        }

        .botao {
            background-color: #4C51BF;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            margin-right: 10px;
            transition: background-color 0.3s ease;
        }

        .botao:hover {
            background-color: #434190;
        }

        .tabela-avaliacoes {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: white;
        }

        .tabela-avaliacoes th, 
        .tabela-avaliacoes td {
            padding: 12px;
            border: 1px solid #dddddd;
            text-align: left;
        }

        .tabela-avaliacoes th {
            background-color: #f8f8f8;
            font-weight: bold;
        }

        .status {
            padding: 15px;
            margin: 15px 0;
            border-radius: 4px;
            font-weight: bold;
        }

        .status.erro {
            background-color: #FEE2E2;
            color: #991B1B;
            border: 1px solid #991B1B;
        }

        .status.sucesso {
            background-color: #DCFCE7;
            color: #166534;
            border: 1px solid #166534;
        }

        select[multiple] {
            height: auto;
            min-height: 100px;
        }

        h1, h2 {
            color: #1a202c;
            margin-bottom: 20px;
        }

        h1 {
            font-size: 24px;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
        }

        h2 {
            font-size: 20px;
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>FAST HUG - Avaliação Diária</h1>
        
        <form id="fastHugForm">
            <div class="form-group">
                <label>Data da Avaliação:</label>
                <input type="date" id="data" required>
            </div>

            <div class="form-group">
                <label>Nome do Paciente:</label>
                <input type="text" id="paciente" required>
            </div>

            <div class="form-group">
                <label>Leito:</label>
                <input type="text" id="leito" required>
            </div>

            <div class="form-group">
                <label>Data de Internação na UTI:</label>
                <input type="date" id="data_internacao_uti" onchange="calcularTempoInternacao()" required>
                <div id="tempo_internacao" style="margin-top: 8px; color: #4a5568; font-weight: bold;"></div>
            </div>

            <div class="form-group">
                <label>Paciente pode ter alta?</label>
                <div class="checkbox-group">
                    <input type="radio" id="alta_sim" name="alta" value="sim" onchange="toggleAlta()">
                    <label for="alta_sim">Sim</label>
                    <input type="radio" id="alta_nao" name="alta" value="nao" onchange="toggleAlta()">
                    <label for="alta_nao">Não</label>
                </div>
                <div id="alta_info" style="display:none; margin-top: 10px;">
                    <textarea 
                        id="observacoes_alta" 
                        placeholder="Observações sobre a alta do paciente"
                        rows="2">
                    </textarea>
                </div>
            </div>

            <div class="form-group">
                <label>Intubado(a)?</label>
                <div class="checkbox-group">
                    <input type="radio" id="intubado_sim" name="intubado" value="sim" onchange="toggleIntubacao()">
                    <label for="intubado_sim">Sim</label>
                    <input type="radio" id="intubado_nao" name="intubado" value="nao" onchange="toggleIntubacao()">
                    <label for="intubado_nao">Não</label>
                </div>
            </div>

            <div id="intubacao_info" style="display:none">
                <div class="form-group">
                    <label>Data da Intubação:</label>
                    <input type="date" id="data_intubacao" onchange="calcularTempoIntubacao()">
                    <div id="tempo_intubacao" style="margin-top: 5px; color: #4a5568; font-weight: bold;"></div>
                </div>
            </div>

            <div class="form-group">
                <label>Uso de Cateter Venoso Central:</label>
                <div class="checkbox-group">
                    <input type="radio" id="cateter_sim" name="cateter" value="sim" onchange="toggleCateter()">
                    <label for="cateter_sim">Sim</label>
                    <input type="radio" id="cateter_nao" name="cateter" value="nao" onchange="toggleCateter()">
                    <label for="cateter_nao">Não</label>
                </div>
            </div>

            <div id="cateter_info" style="display:none">
                <div class="form-group">
                    <label>Localização do Cateter:</label>
                    <select id="localizacao_cateter" class="form-select">
                        <option value="">Selecione a localização</option>
                        <option value="jugular">Jugular</option>
                        <option value="subclavia">Subclávia</option>
                        <option value="femoral">Femoral</option>
                    </select>
                </div>

                <div class="form-group">
                    <label>Data de Inserção do Cateter:</label>
                    <input type="date" id="data_cateter" onchange="calcularTempoCateter()">
                    <div id="tempo_cateter" style="margin-top: 8px; color: #4a5568; font-weight: bold;"></div>
                </div>

                <div class="form-group">
                    <label>Pode ser retirado?</label>
                    <div class="checkbox-group">
                        <input type="radio" id="retirar_sim" name="retirar_cateter" value="sim">
                        <label for="retirar_sim">Sim</label>
                        <input type="radio" id="retirar_nao" name="retirar_cateter" value="nao">
                        <label for="retirar_nao">Não</label>
                    </div>
                </div>
            </div>
            function toggleVentilacao() {
    const vmInfo = document.getElementById('vm_info');
    const vniInfo = document.getElementById('vni_info');
    const cnInfo = document.getElementById('cn_info');
    
    // Esconde todos primeiro
    vmInfo.style.display = 'none';
    vniInfo.style.display = 'none';
    cnInfo.style.display = 'none';
    
    // Mostra apenas o selecionado
    if (document.getElementById('ventilacao_vm').checked) {
        vmInfo.style.display = 'block';
    } else if (document.getElementById('ventilacao_vni').checked) {
        vniInfo.style.display = 'block';
    } else if (document.getElementById('ventilacao_cn').checked) {
        cnInfo.style.display = 'block';
    }
}

// Adicionar ao evento de submit do formulário:
document.getElementById('fastHugForm').addEventListener('submit', function(evento) {
    // ... resto do código ...
    
    const novaAvaliacao = {
        // ... outros campos ...
        tipo_ventilacao: document.querySelector('input[name="tipo_ventilacao"]:checked')?.value,
        parametros_vm: document.getElementById('ventilacao_vm').checked ? {
            modo: document.getElementById('modo_ventilatorio').value,
            fio2: document.getElementById('fio2').value,
            peep: document.getElementById('peep').value,
            volume_corrente: document.getElementById('volume_corrente').value,
            fr_total: document.getElementById('fr_total').value,
            pressao_pico: document.getElementById('pressao_pico').value,
            desmame: document.querySelector('input[name="desmame"]:checked')?.value
        } : null,
        parametros_vni: document.getElementById('ventilacao_vni').checked ? {
            ipap: document.getElementById('ipap').value,
            epap: document.getElementById('epap').value,
            fio2: document.getElementById('fio2_vni').value
        } : null,
        fluxo_o2: document.getElementById('ventilacao_cn').checked ? 
            document.getElementById('fluxo_o2').value : null
    };
                <!-- Seção de Monitorização -->
            <div class="form-group">
                <label>Monitorização:</label>
                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; margin-top: 10px;">
                    <!-- Sinais Vitais -->
                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Sinais Vitais</h3>
                        <div style="display: grid; gap: 10px;">
                            <div>
                                <label>PA (mmHg):</label>
                                <div style="display: flex; gap: 5px;">
                                    <input type="number" id="pa_sistolica" placeholder="PAS" min="0" max="300" style="width: 80px;">
                                    <span style="align-self: center;">/</span>
                                    <input type="number" id="pa_diastolica" placeholder="PAD" min="0" max="300" style="width: 80px;">
                                </div>
                            </div>
                            <div>
                                <label>FC (bpm):</label>
                                <input type="number" id="fc" min="0" max="300">
                            </div>
                            <div>
                                <label>FR (irpm):</label>
                                <input type="number" id="fr" min="0" max="100">
                            </div>
                            <div>
                                <label>Temperatura (°C):</label>
                                <input type="number" id="temperatura" min="30" max="45" step="0.1">
                            </div>
                        </div>
                    </div>

                    <!-- Oximetria e Gases -->
                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Oximetria e Gases</h3>
                        <div style="display: grid; gap: 10px;">
                            <div>
                                <label>SpO2 (%):</label>
                                <input type="number" id="spo2" min="0" max="100">
                            </div>
                            <div>
                                <label>Lactato:</label>
                                <input type="number" id="lactato" min="0" max="50" step="0.1">
                            </div>
                            <div>
                                <label>pH:</label>
                                <input type="number" id="ph" min="6.5" max="8.0" step="0.01">
                            </div>
                            <div>
                                <label>HCO3:</label>
                                <input type="number" id="hco3" min="0" max="50" step="0.1">
                            </div>
                        </div>
                    </div>

                    <!-- Neurológico -->
                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Avaliação Neurológica</h3>
                        <div style="display: grid; gap: 10px;">
                            <div>
                                <label>Escala de Glasgow:</label>
                                <input type="number" id="glasgow" min="3" max="15">
                            </div>
                            <div>
                                <label>RASS:</label>
                                <select id="rass">
                                    <option value="">Selecione</option>
                                    <option value="+4">+4 Combativo</option>
                                    <option value="+3">+3 Muito agitado</option>
                                    <option value="+2">+2 Agitado</option>
                                    <option value="+1">+1 Inquieto</option>
                                    <option value="0">0 Alerta/Calmo</option>
                                    <option value="-1">-1 Sonolento</option>
                                    <option value="-2">-2 Sedação leve</option>
                                    <option value="-3">-3 Sedação moderada</option>
                                    <option value="-4">-4 Sedação profunda</option>
                                    <option value="-5">-5 Não desperta</option>
                                </select>
                            </div>
                            <div>
                                <label>Pupilas:</label>
                                <select id="pupilas">
                                    <option value="">Selecione</option>
                                    <option value="iso_foto">Isocóricas e fotorreagentes</option>
                                    <option value="aniso_foto">Anisocóricas e fotorreagentes</option>
                                    <option value="iso_nao_foto">Isocóricas e não fotorreagentes</option>
                                    <option value="aniso_nao_foto">Anisocóricas e não fotorreagentes</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- Hemodinâmica -->
                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Monitorização Hemodinâmica</h3>
                        <div style="display: grid; gap: 10px;">
                            <div>
                                <label>PAM (mmHg):</label>
                                <input type="number" id="pam" min="0" max="200">
                            </div>
                            <div>
                                <label>PVC (mmHg):</label>
                                <input type="number" id="pvc" min="0" max="50">
                            </div>
                            <div>
                                <label>Débito Urinário (mL/h):</label>
                                <input type="number" id="debito_urinario" min="0">
                            </div>
                            <div>
                                <label>Balanço Hídrico (mL):</label>
                                <input type="number" id="balanco_hidrico">
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Drogas Vasoativas -->
                <div class="card" style="padding: 15px; margin-top: 15px;">
                    <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Drogas Vasoativas</h3>
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px;">
                        <div>
                            <label>Noradrenalina (mcg/kg/min):</label>
                            <input type="number" id="noradrenalina" min="0" max="5" step="0.01">
                        </div>
                        <div>
                            <label>Dobutamina (mcg/kg/min):</label>
                            <input type="number" id="dobutamina" min="0" max="50" step="0.1">
                        </div>
                        <div>
                            <label>Vasopressina (U/min):</label>
                            <input type="number" id="vasopressina" min="0" max="0.1" step="0.01">
                        </div>
                    </div>
                </div>
            </div>
                        <!-- Seção F - Feeding (Nutrição) -->
            <div class="form-group">
                <label>F - Alimentação:</label>
                <div class="checkbox-group">
                    <input type="radio" id="nutricao_enteral" name="tipo_nutricao" value="enteral" onchange="toggleNutricao()">
                    <label for="nutricao_enteral">Nutrição Enteral</label>
                    
                    <input type="radio" id="nutricao_parenteral" name="tipo_nutricao" value="parenteral" onchange="toggleNutricao()">
                    <label for="nutricao_parenteral">Nutrição Parenteral</label>
                    
                    <input type="radio" id="nutricao_vo" name="tipo_nutricao" value="vo" onchange="toggleNutricao()">
                    <label for="nutricao_vo">Via Oral</label>
                    
                    <input type="radio" id="nutricao_jejum" name="tipo_nutricao" value="jejum" onchange="toggleNutricao()">
                    <label for="nutricao_jejum">Jejum</label>
                </div>

                <div id="nutricao_info" style="display:none; margin-top: 10px;">
                    <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px;">
                        <div>
                            <label>Volume em 24h (mL):</label>
                            <input type="number" id="volume_nutricao" min="0">
                        </div>
                        <div>
                            <label>Velocidade de Infusão (mL/h):</label>
                            <input type="number" id="velocidade_nutricao" min="0">
                        </div>
                    </div>
                </div>
            </div>

            <!-- Seção A - Analgesia -->
            <div class="form-group">
                <label>A - Analgesia:</label>
                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px;">
                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Medicações em Uso</h3>
                        <div class="checkbox-group">
                            <div>
                                <input type="checkbox" id="analgesico_dipirona" name="analgesicos">
                                <label for="analgesico_dipirona">Dipirona</label>
                            </div>
                            <div>
                                <input type="checkbox" id="analgesico_tramadol" name="analgesicos">
                                <label for="analgesico_tramadol">Tramadol</label>
                            </div>
                            <div>
                                <input type="checkbox" id="analgesico_morfina" name="analgesicos">
                                <label for="analgesico_morfina">Morfina</label>
                            </div>
                            <div>
                                <input type="checkbox" id="analgesico_fentanil" name="analgesicos">
                                <label for="analgesico_fentanil">Fentanil</label>
                            </div>
                        </div>
                    </div>

                    <div class="card" style="padding: 15px; margin: 0;">
                        <h3 style="margin-top: 0; color: #4a5568; font-size: 16px;">Avaliação da Dor</h3>
                        <div>
                            <label>Escala de Dor (0-10):</label>
                            <input type="number" id="escala_dor" min="0" max="10">
                        </div>
                    </div>
                </div>
            </div>

            <!-- Seção S - Sedação -->
            <div class="form-group">
                <label>S - Sedação:</label>
                <div class="checkbox-group">
                    <div>
                        <input type="checkbox" id="sedacao_midazolam" name="sedativos">
                        <label for="sedacao_midazolam">Midazolam</label>
                        <input type="number" id="dose_midazolam" placeholder="mg/h" min="0" style="width: 80px; margin-left: 10px;">
                    </div>
                    <div>
                        <input type="checkbox" id="sedacao_fentanil" name="sedativos">
                        <label for="sedacao_fentanil">Fentanil</label>
                        <input type="number" id="dose_fentanil" placeholder="mcg/h" min="0" style="width: 80px; margin-left: 10px;">
                    </div>
                    <div>
                        <input type="checkbox" id="sedacao_propofol" name="sedativos">
                        <label for="sedacao_propofol">Propofol</label>
                        <input type="number" id="dose_propofol" placeholder="mg/h" min="0" style="width: 80px; margin-left: 10px;">
                    </div>
                    <div>
                        <input type="checkbox" id="sedacao_dexmedetomidina" name="sedativos">
                        <label for="sedacao_dexmedetomidina">Dexmedetomidina</label>
                        <input type="number" id="dose_dexmedetomidina" placeholder="mcg/kg/h" min="0" style="width: 80px; margin-left: 10px;">
                    </div>
                </div>
            </div>

            <!-- Seção T - Tromboprofilaxia -->
            <div class="form-group">
                <label>T - Tromboprofilaxia:</label>
                <div class="checkbox-group">
                    <div style="margin-bottom: 8px;">
                        <input type="checkbox" id="hbpm" name="tromboprofilaxia">
                        <label for="hbpm">HBPM (Heparina de Baixo Peso Molecular)</label>
                    </div>
                    <div style="margin-bottom: 8px;">
                        <input type="checkbox" id="hnf" name="tromboprofilaxia">
                        <label for="hnf">HNF (Heparina Não Fracionada)</label>
                    </div>
                    <div style="margin-bottom: 8px;">
                        <input type="checkbox" id="aco" name="tromboprofilaxia">
                        <label for="aco">ACO (Anticoagulante Oral)</label>
                    </div>
                    <div style="margin-bottom: 8px;">
                        <input type="checkbox" id="meias" name="tromboprofilaxia">
                        <label for="meias">Meias Elásticas</label>
                    </div>
                </div>
                <textarea 
                    id="tromboprofilaxia_obs" 
                    placeholder="Observações sobre tromboprofilaxia: dosagem, contraindicações, etc."
                    rows="3">
                </textarea>
            </div>

            <!-- Seção H - Head of Bed Elevation -->
            <div class="form-group">
                <label>H - Cabeceira Elevada:</label>
                <div class="checkbox-group">
                    <input type="radio" id="cabeceira_30" name="cabeceira" value="30">
                    <label for="cabeceira_30">30°</label>
                    
                    <input type="radio" id="cabeceira_45" name="cabeceira" value="45">
                    <label for="cabeceira_45">45°</label>
                    
                    <input type="radio" id="cabeceira_0" name="cabeceira" value="0">
                    <label for="cabeceira_0">0° (Contraindicado)</label>
                </div>
                <textarea 
                    id="cabeceira_obs" 
                    placeholder="Observações sobre posicionamento do paciente"
                    rows="2">
                </textarea>
            </div>

            <!-- Seção U - Úlcera de Estresse -->
            <div class="form-group">
                <label>U - Profilaxia de Úlcera de Estresse:</label>
                <div class="checkbox-group">
                    <div>
                        <input type="checkbox" id="ulcera_omeprazol" name="protecao_gastrica">
                        <label for="ulcera_omeprazol">Omeprazol</label>
                    </div>
                    <div>
                        <input type="checkbox" id="ulcera_ranitidina" name="protecao_gastrica">
                        <label for="ulcera_ranitidina">Ranitidina</label>
                    </div>
                    <div>
                        <input type="checkbox" id="ulcera_pantoprazol" name="protecao_gastrica">
                        <label for="ulcera_pantoprazol">Pantoprazol</label>
                    </div>
                </div>
            </div>

            <!-- Seção G - Glicemia -->
            <div class="form-group">
                <label>G - Glicemia:</label>
                <input 
                    type="number" 
                    id="glicemia" 
                    placeholder="Valor da glicemia em mg/dL"
                    min="0" 
                    max="999">
                
                <div class="checkbox-group" style="margin-top: 10px;">
                    <input type="radio" id="insulina_sim" name="recebeu_insulina" value="sim" onchange="toggleInsulinaQuantidade()">
                    <label for="insulina_sim">Recebeu Insulina: Sim</label>
                    
                    <input type="radio" id="insulina_nao" name="recebeu_insulina" value="nao" onchange="toggleInsulinaQuantidade()">
                    <label for="insulina_nao">Recebeu Insulina: Não</label>
                </div>

                <div id="insulina_info" style="display: none; margin-top: 10px;">
                    <label>Quantidade de Insulina (UI):</label>
                    <input 
                        type="number" 
                        id="quantidade_insulina" 
                        placeholder="Unidades de Insulina"
                        min="0" 
                        step="1" 
                        class="w-full p-2 border rounded">
                </div>
            </div>

            <!-- Botão de Envio -->
            <div class="form-group" style="margin-top: 20px;">
                <button type="submit" class="botao">Salvar Avaliação</button>
            </div>
        </form>
    </div>
    
