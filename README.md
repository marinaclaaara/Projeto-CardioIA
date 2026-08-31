# Projeto-CardioIA

# CardioIA — Fase 1: Batimentos de Dados

**Projeto:** CardioIA — A Nova Era da Cardiologia Inteligente
**Fase:** 1 de 7 — Batimentos de Dados (Mapeando o Coração Moderno)
**Papel assumido:** Cientista de Dados Hospitalar
**Autoria:** Marina Clara Constantino Ribeiro

Todos os dados numéricos e de imagem desta entrega são **dados reais**, de pacientes de verdade, coletados de bases públicas com licença que permite uso e redistribuição acadêmica. As fontes e a autenticidade de cada base foram checadas manualmente byte a byte contra o arquivo original publicado pelos autores (ver seção "Verificação de autenticidade" ao final).

## Estrutura do repositório

```
├── README.md
├── dataset_cardiaco_real_uci.csv        # Parte 1 - dados numéricos REAIS
├── docs/
│   └── LEIA-ME_textos.txt               # Parte 2 - instruções + links reais
└── assets/
    ├── imagens_ecg_reais.zip            # Parte 3 - 140 imagens REAIS de ECG
    └── metadata_ecg_real.csv            # rótulo de cada imagem + nome original
```

> **Link público dos dados completos:** https://drive.google.com/drive/folders/1dUG8VIU7WskOGRUI_EvyJF6koOciCQaI

---

## Parte 1 — Dados Numéricos (IoT) — REAIS

**Arquivo:** `dataset_cardiaco_real_uci.csv` (303 pacientes, 15 colunas)

**Origem:** *Heart Disease Dataset*, UCI Machine Learning Repository — dados reais de pacientes coletados pela Cleveland Clinic Foundation (EUA), doados por Robert Detrano, M.D., Ph.D. Identificadores pessoais já removidos pelos próprios curadores originais.
Fonte: https://archive.ics.uci.edu/dataset/45/heart+disease
Licença: **CC BY 4.0**.
Citação: Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). *Heart Disease* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C52P4X

**Variáveis:**

| Coluna | Descrição | Relevância clínica |
|---|---|---|
| age | idade do paciente | principal fator de risco cardiovascular |
| sex | sexo (1=M, 0=F) | risco cardiovascular difere por sexo |
| cp | tipo de dor no peito (1–4: angina típica, atípica, não-anginosa, assintomático) | sintoma-chave de triagem |
| trestbps | pressão arterial em repouso (mmHg) | hipertensão é o principal fator de risco modificável |
| chol | colesterol sérico (mg/dl) | associado a aterosclerose e infarto |
| fbs | glicemia em jejum > 120 mg/dl | associação com diabetes/risco cardiovascular |
| restecg | resultado do ECG em repouso (0=normal, 1=anormalidade ST-T, 2=hipertrofia ventricular) | indica alterações estruturais/elétricas |
| thalach | frequência cardíaca **máxima atingida em teste de esforço** | capacidade cardiovascular sob estresse |
| exang | angina induzida por exercício | indicador de isquemia |
| oldpeak / slope | depressão do segmento ST | marcador clássico de isquemia miocárdica |
| ca | nº de vasos principais visíveis (fluoroscopia, 0–3) | gravidade da doença coronariana |
| thal | talassemia (3=normal, 6=defeito fixo, 7=defeito reversível) | usado em conjunto com outros exames |
| num | grau original de doença (0=ausência, 1–4=graus de presença) | variável bruta publicada pela UCI |
| **target** | versão binária de `num` (0=ausência, 1=presença) | **rótulo-alvo para os classificadores da Fase 2** |

> **Observação importante:** o enunciado cita "sintomas" e "frequência cardíaca" como exemplos de variáveis — este dataset real não tem uma coluna literal de texto livre com sintomas nem a frequência cardíaca de repouso; os proxies clínicos equivalentes disponíveis são `cp` e `exang` (sintomas de dor no peito/angina) e `thalach` (frequência cardíaca sob esforço). Isso está registrado aqui para deixar claro que não inventei nenhuma coluna — usei exatamente o que existe na base real.

---

## Parte 2 — Dados Textuais (NLP) — AÇÃO PENDENTE (não posso baixar por você)

Duas fontes **reais e oficiais**, com link verificado e funcionando:

1. *Prevenção Clínica de Doença Cardiovascular, Cerebrovascular e Renal* — Caderno de Atenção Básica nº 14, Ministério da Saúde/BVS.
   https://bvsms.saude.gov.br/bvs/publicacoes/abcad14.pdf
2. *Saúde do Coração* — Boletim Temático nº 9, set/2022, Ministério da Saúde/BVS.
   https://bvsms.saude.gov.br/bvs/boletim_tematico/saude_coracao_setembro_2022.pdf


---

## Parte 3 — Dados Visuais (Visão Computacional) — REAIS

**Arquivo:** `assets/imagens_ecg_reais.zip` — **140 imagens reais** de exames de ECG de 12 derivações, de pacientes de verdade (anonimizados). 

**Origem:** *ECG Images dataset of Cardiac and COVID-19 Patients*, Khan, A.H.; Hussain, M.; Malik, M.K. (2021). *Data in Brief*, v.34, DOI: 10.1016/j.dib.2021.106762. Dados coletados com o dispositivo EDAN SERIES-3 em três hospitais no Paquistão (Ch. Pervaiz Elahi Institute of Cardiology, Nishtar Hospital, Punjab Institute of Cardiology), revisados por profissionais médicos.
Repositório de origem: https://data.mendeley.com/datasets/gwbz3fsgp8/1
Licença: **CC BY 4.0** — imagens já anonimizadas pelos autores originais.

Amostra de 140 imagens (de ~928 disponíveis), balanceada em 4 categorias reais de diagnóstico:

| Categoria | Imagens disponíveis na base original | Imagens na amostra |
|---|---|---|
| Normal | 284 | 35 |
| Infarto do miocárdio (MI) | 239 | 35 |
| Histórico de infarto do miocárdio | 172 | 35 |
| Batimento cardíaco anormal | 233 | 35 |

O rótulo de cada imagem e o nome do arquivo original na base estão em `metadata_ecg_real.csv`.

## Governança de Dados e Vieses (reflexão)

- O dataset numérico (UCI/Cleveland) é de pacientes americanos avaliados nos anos 1980 — pode não refletir perfis epidemiológicos atuais nem a população brasileira.
- O dataset de imagens de ECG é de pacientes paquistaneses de três hospitais de uma mesma região (Punjab) — um modelo treinado só nele pode não generalizar bem para outras etnias, faixas etárias ou equipamentos de ECG diferentes.
- Ambos os datasets já vieram anonimizados pelos autores originais; ainda assim, é importante documentar a licença (CC BY 4.0) e citar a autoria em qualquer uso posterior.
- Os textos institucionais (BVS/Ministério da Saúde), quando baixados, refletem a realidade epidemiológica brasileira e complementam os dados de imagem/numéricos, que são de outros países.

## Autoria

Marina Clara Constantino Ribeiro — Atividade avaliativa CardioIA, Fase 1.
