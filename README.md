<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Avaliação Inicial UTI</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }

        body {
            background-color: #f3f4f6;
            padding: 20px;
        }

        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            padding: 20px;
            max-width: 1000px;
            margin: 0 auto 20px auto;
        }

        h1 {
            color: #1e40af;
            text-align: center;
            margin-bottom: 20px;
            font-size: 24px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .section-title {
            color: #1e40af;
            font-size: 18px;
            margin-bottom: 10px;
            padding-bottom: 5px;
            border-bottom: 2px solid #e2e8f0;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #374151;
        }

        input[type="text"],
        input[type="date"],
        input[type="number"],
        select,
        textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #d1d5db;
            border-radius: 4px;
            font-size: 16px;
        }

        .grid-2 {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .grid-3 {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
        }

        .checkbox-group {
            display: flex;
            gap: 15px;
            margin-top: 5px;
        }

        .checkbox-container {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .info-box {
            background-color: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 4px;
            padding: 10px;
            margin-top: 5px;
        }

        .botoes {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        .botao {
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        .botao-primario {
            background-color: #1e40af;
            color: white;
        }

        .botao-secundario {
            background-color: #4b5563;
            color: white;
        }

        .botao:hover {
            opacity: 0.9;
        }

        @media (max-width: 768px) {
            .grid-2, .grid-3 {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Avaliação Inicial UTI</h1>
        
        <form id="avaliacaoForm">
            <!-- Identificação -->
            <div class="form-group">
                <h2 class="section-title">Identificação do Paciente</h2>
                <div class="grid-2">
                    <div>
                        <label>Nome do Paciente:</label>
                        <input type="text" id="nome" name="nome" required>
                    </div>
                    <div>
                        <label>Registro:</label>
                        <input type="text" id="registro" name="registro" required>
                    </div>
                </div>
                <div class="grid-3">
                    <div>
                        <label>Sexo:</label>
                        <select id="sexo" name="sexo" required>
                            <option value="">Selecione</option>
                            <option value="M">Masculino</option>
                            <option value="F">Feminino</option>
                        </select>
                    </div>
                    <div>
                        <label>Data de Internação:</label>
                        <input type="date" id="data_internacao" name="data_internacao" onchange="calcularTempoInternacao()" required>
                        <div id="tempo_internacao" class="info-box"></div>
                    </div>
                    <div>
                        <label>Leito:</label>
                        <input type="text" id="leito" name="leito" required>
                    </div>
                </div>
            </div>

            <!-- Alimentação -->
            <div class="form-group">
                <h2 class="section-title">Alimentação</h2>
                <div class="grid-2">
                    <div>
                        <label>Via de Alimentação:</label>
                        <select id="via_alimentacao" name="via_alimentacao" onchange="toggleAlimentacao()">
                            <option value="">Selecione</option>
                            <option value="oral">Via Oral</option>
                            <option value="sng">SNG</option>
                            <option value="sne">SNE</option>
                            <option value="gastrostomia">Gastrostomia</option>
                            <option value="jejunostomia">Jejunostomia</option>
                            <option value="npo">NPO</option>
                        </select>
                    </div>
                    <div id="dieta_info" style="display: none;">
                        <label>Tipo de Dieta:</label>
                        <select id="tipo_dieta" name="tipo_dieta">
                            <option value="">Selecione</option>
                            <option value="padrao">Padrão</option>
                            <option value="branda">Branda</option>
                            <option value="pastosa">Pastosa</option>
                            <option value="liquida">Líquida</option>
                            <option value="enteral">Enteral</option>
                        </select>
                    </div>
                </div>
                <div id="volume_info" style="display: none; margin-top: 10px;">
                    <label>Volume em 24h (mL):</label>
                    <input type="number" id="volume_dieta" name="volume_dieta">
                </div>
            </div>

            <!-- Analgesia -->
            <div class="form-group">
                <h2 class="section-title">Analgesia</h2>
                <div class="grid-2">
                    <div>
                        <label>Analgésicos em Uso:</label>
                        <div class="checkbox-container">
                            <input type="checkbox" id="dipirona" name="analgesicos" value="dipirona">
                            <label for="dipirona">Dipirona</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="tramadol" name="analgesicos" value="tramadol">
                            <label for="tramadol">Tramadol</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="morfina" name="analgesicos" value="morfina">
                            <label for="morfina">Morfina</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="fentanil" name="analgesicos" value="fentanil">
                            <label for="fentanil">Fentanil</label>
                        </div>
                    </div>
                    <div>
                        <label>Escala de Dor (0-10):</label>
                        <input type="number" id="escala_dor" name="escala_dor" min="0" max="10">
                    </div>
                </div>
            </div>

            <!-- Sedação -->
            <div class="form-group">
                <h2 class="section-title">Sedação</h2>
                <div class="grid-2">
                    <div>
                        <label>Sedativos em Uso:</label>
                        <div class="checkbox-container">
                            <input type="checkbox" id="midazolam" name="sedativos" value="midazolam">
                            <label for="midazolam">Midazolam</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="propofol" name="sedativos" value="propofol">
                            <label for="propofol">Propofol</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="dexmedetomidina" name="sedativos" value="dexmedetomidina">
                            <label for="dexmedetomidina">Dexmedetomidina</label>
                        </div>
                    </div>
                    <div>
                        <label>RASS:</label>
                        <select id="rass" name="rass">
                            <option value="">Selecione</option>
                            <option value="+4">+4 Combativo</option>
                            <option value="+3">+3 Muito agitado</option>
                            <option value="+2">+2 Agitado</option>
                            <option value="+1">+1 Inquieto</option>
                            <option value="0">0 Alerta e calmo</option>
                            <option value="-1">-1 Sonolento</option>
                            <option value="-2">-2 Sedação leve</option>
                            <option value="-3">-3 Sedação moderada</option>
                            <option value="-4">-4 Sedação profunda</option>
                            <option value="-5">-5 Não despertável</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Tromboprofilaxia -->
            <div class="form-group">
                <h2 class="section-title">Tromboprofilaxia</h2>
                <div class="grid-2">
                    <div>
                        <label>Profilaxia em Uso:</label>
                        <select id="tromboprofilaxia" name="tromboprofilaxia">
                            <option value="">Selecione</option>
                            <option value="heparina">Heparina não fracionada</option>
                            <option value="enoxaparina">Enoxaparina</option>
                            <option value="mecanica">Profilaxia mecânica</option>
                            <option value="contraindicada">Contraindicada</option>
                            <option value="nao">Não está em uso</option>
                        </select>
                    </div>
                    <div>
                        <label>Observações:</label>
                        <textarea id="obs_tromboprofilaxia" name="obs_tromboprofilaxia" rows="2"></textarea>
                    </div>
                </div>
            </div>

            <!-- Cabeceira e Conforto -->
            <div class="form-group">
                <h2 class="section-title">Cabeceira e Conforto</h2>
                <div class="grid-2">
                    <div>
                        <label>Cabeceira (graus):</label>
                        <input type="number" id="cabeceira" name="cabeceira" min="0" max="90">
                    </div>
                    <div>
                        <label>Mudança de Decúbito:</label>
                        <select id="mudanca_decubito" name="mudanca_decubito">
                            <option value="">Selecione</option>
                            <option value="2/2h">2/2h</option>
                            <option value="4/4h">4/4h</option>
                            <option value="nao_programada">Não programada</option>
                            <option value="contraindicada">Contraindicada</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Proteção Gástrica -->
            <div class="form-group">
                <h2 class="section-title">Proteção Gástrica</h2>
                <div class="grid-2">
                    <div>
                        <label>Medicação em Uso:</label>
                        <select id="protecao_gastrica" name="protecao_gastrica">
                            <option value="">Selecione</option>
                            <option value="omeprazol">Omeprazol</option>
                            <option value="ranitidina">Ranitidina</option>
                            <option value="pantoprazol">Pantoprazol</option>
                            <option value="nao">Não está em uso</option>
                        </select>
                    </div>
                    <div>
                        <label>Indicação:</label>
                        <input type="text" id="indicacao_protecao" name="indicacao_protecao">
                    </div>
                </div>
            </div>

            <!-- Controle Glicêmico -->
            <div class="form-group">
                <h2 class="section-title">Controle Glicêmico</h2>
                <div class="grid-3">
                    <div>
                        <label>Última Glicemia (mg/dL):</label>
                        <input type="number" id="glicemia" name="glicemia">
                    </div>
                    <div>
                        <label>Insulina em Uso:</label>
                        <select id="insulina" name="insulina">
                            <option value="">Selecione</option>
                            <option value="regular">Regular</option>
                            <option value="nph">NPH</option>
                            <option value="ambas">Ambas</option>
                            <option value="nao">Não está em uso</option>
                        </select>
                    </div>
                    <div>
                        <label>Esquema:</label>
                        <select id="esquema_insulina" name="esquema_insulina">
                            <option value="">Selecione</option>
                            <option value="fixo">Fixo</option>
                            <option value="sliding">Sliding Scale</option>
                            <option value="bomba">Bomba de infusão</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Teste de Respiração Espontânea -->
            <div class="form-group">
                <h2 class="section-title">Teste de Respiração Espontânea</h2>
                <div class="grid-2">
                    <div>
                        <label>Elegível para TRE:</label>
                        <select id="tre_elegivel" name="tre_elegivel">
                            <option value="">Selecione</option>
                            <option value="sim">Sim</option>
                            <option value="nao">Não</option>
                        </select>
                    </div>
                    <div>
                        <label>Motivo se não elegível:</label>
                        <input type="text" id="tre_motivo" name="tre_motivo">
                    </div>
                </div>
            </div>

            <!-- Trânsito Intestinal -->
            <div class="form-group">
                <h2 class="section-title">Trânsito Intestinal</h2>
                <div class="grid-2">
                    <div>
                        <label>Última Evacuação:</label>
                        <input type="date" id="ultima_evacuacao" name="ultima_evacuacao">
                    </div>
                    <div>
                        <label>Laxativos em Uso:</label>
                        <div class="checkbox-container">
                            <input type="checkbox" id="lactulose" name="laxativos" value="lactulose">
                            <label for="lactulose">Lactulose</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="bisacodil" name="laxativos" value="bisacodil">
                            <label for="bisacodil">Bisacodil</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="fleet" name="laxativos" value="fleet">
                            <label for="fleet">Fleet</label>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Cateteres e Sondas -->
            <div class="form-group">
                <h2 class="section-title">Cateteres e Sondas</h2>
                <div class="grid-2">
                    <div>
                        <label>Dispositivos em Uso:</label>
                        <div class="checkbox-container">
                            <input type="checkbox" id="cvc" name="dispositivos" value="cvc">
                            <label for="cvc">CVC</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="svd" name="dispositivos" value="svd">
                            <label for="svd">SVD</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="sng" name="dispositivos" value="sng">
                            <label for="sng">SNG</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="sne" name="dispositivos" value="sne">
                            <label for="sne">SNE</label>
                        </div>
                        <div class="checkbox-container">
                            <input type="checkbox" id="dreno" name="dispositivos" value="dreno">
                            <label for="dreno">Dreno</label>
                        </div>
                    </div>
                    <div>
                        <label>Data de Inserção CVC:</label>
                        <input type="date" id="data_cvc" name="data_cvc">
                        <div id="tempo_cvc" class="info-box"></div>
                    </div>
                </div>
            </div>

            <!-- Antibióticos -->
            <div class="form-group">
                <h2 class="section-title">Antibióticos</h2>
                <div class="grid-2">
                    <div>
                        <label>Em Uso de ATB:</label>
                        <select id="uso_atb" name="uso_atb" onchange="toggleAtb()">
                            <option value="">Selecione</option>
                            <option value="sim">Sim</option>
                            <option value="nao">Não</option>
                        </select>
                    </div>
                    <div id="atb_info" style="display: none;">
                        <label>Indicação:</label>
                        <input type="text" id="indicacao_atb" name="indicacao_atb">
                    </div>
                </div>
                <div id="atb_dias" style="display: none; margin-top: 10px;">
                    <label>Dia do ATB:</label>
                    <input type="number" id="dia_atb" name="dia_atb">
                </div>
            </div>
        </form>

        <div class="botoes">
            <button type="button" class="botao botao-primario" onclick="salvarAvaliacao()">Salvar Avaliação</button>
            <button type="button" class="botao botao-secundario" onclick="exportarCSV()">Exportar CSV</button>
        </div>
    </div>

    <script>
        function calcularTempoInternacao() {
            const dataInternacao = new Date(document.getElementById('data_internacao').value);
            const hoje = new Date();
            const diffTempo = Math.abs(hoje - dataInternacao);
            const diffDias = Math.ceil(diffTempo / (1000 * 60 * 60 * 24));
            
            document.getElementById('tempo_internacao').innerHTML = 
                `Tempo de internação: ${diffDias} dia(s)`;
        }

        function toggleAlimentacao() {
            const via = document.getElementById('via_alimentacao').value;
            const dietaInfo = document.getElementById('dieta_info');
            const volumeInfo = document.getElementById('volume_info');
            
            dietaInfo.style.display = via === 'npo' ? 'none' : 'block';
            volumeInfo.style.display = (via === 'sng' || via === 'sne' || via === 'gastrostomia' || via === 'jejunostomia') ? 'block' : 'none';
        }

        function toggleAtb() {
            const usoAtb = document.getElementById('uso_atb').value;
            const atbInfo = document.getElementById('atb_info');
            const atbDias = document.getElementById('atb_dias');
            
            atbInfo.style.display = usoAtb === 'sim' ? 'block' : 'none';
            atbDias.style.display = usoAtb === 'sim' ? 'block' : 'none';
        }

        function salvarAvaliacao() {
            const form = document.getElementById('avaliacaoForm');
            const formData = new FormData(form);
            const data = {};
            
            for (let [key, value] of formData.entries()) {
                data[key] = value;
            }
            
            // Adicionar checkbox groups
            const checkboxGroups = ['analgesicos', 'sedativos', 'laxativos', 'dispositivos'];
            checkboxGroups.forEach(group => {
                data[group] = Array.from(document.querySelectorAll(`input[name="${group}"]:checked`))
                    .map(cb => cb.value)
                    .join(', ');
            });

            // Salvar no localStorage
            const avaliacoes = JSON.parse(localStorage.getItem('avaliacoes') || '[]');
            avaliacoes.push({
                ...data,
                timestamp: new Date().toISOString()
            });
            localStorage.setItem('avaliacoes', JSON.stringify(avaliacoes));

            alert('Avaliação salva com sucesso!');
            form.reset();
        }

        function exportarCSV() {
            const avaliacoes = JSON.parse(localStorage.getItem('avaliacoes') || '[]');
            if (avaliacoes.length === 0) {
                alert('Não há avaliações para exportar');
                return;
            }

            // Criar cabeçalho CSV
            const headers = Object.keys(avaliacoes[0]);
            let csvContent = headers.join(',') + '\n';

            // Adicionar dados
            avaliacoes.forEach(avaliacao => {
                const row = headers.map(header => {
                    let value = avaliacao[header] || '';
                    // Escapar valores com vírgulas
                    if (value.includes(',')) {
                        value = `"${value}"`;
                    }
                    return value;
                });
                csvContent += row.join(',') + '\n';
            });

            // Criar e baixar arquivo
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', 'avaliacoes_uti.csv');
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        // Calcular tempo de CVC quando a data é alterada
        document.getElementById('data_cvc').addEventListener('change', function() {
            const dataCVC = new Date(this.value);
            const hoje = new Date();
            const diffTempo = Math.abs(hoje - dataCVC);
            const diffDias = Math.ceil(diffTempo / (1000 * 60 * 60 * 24));
            
            document.getElementById('tempo_cvc').innerHTML = 
                `Tempo de CVC: ${diffDias} dia(s)`;
        });
    </script>
</body>
</html>
    
