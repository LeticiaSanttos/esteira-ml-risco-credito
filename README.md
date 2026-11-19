# Esteira de Aprendizado de Máquina — Previsão de Risco de Crédito

Este projeto implementa uma esteira completa de Machine Learning (end-to-end) para resolver um problema de classificação binária no setor financeiro: prever se um cliente apresentará inadimplência grave (atraso igual ou superior a 90 dias) nos próximos dois anos.

## Sobre a Base de Dados
* **Conjunto de Dados:** Give Me Some Credit (`cs-training.csv`)
* **Origem:** [Kaggle Datasets](https://www.kaggle.com/datasets/lihxlhx/give-me-some-credit/data)
* **Variável Alvo:** `SeriousDlqin2yrs` (`0` = Bom Pagador | `1` = Inadimplente)

## Etapas da Esteira Implementada
1. **Aquisição Automatizada:** Download e carregamento do conjunto de dados diretamente do Kaggle via biblioteca `kagglehub`.
2. **Análise Descritiva:** Inspeção da estrutura (150.000 registros e 12 colunas), tipos de variáveis, valores ausentes e desbalanceamento das classes (~93,3% de bons pagadores contra ~6,7% de inadimplentes).
3. **Transformação de Colunas:**
   * Remoção da coluna identificadora (`Unnamed: 0`).
   * Preenchimento de valores nulos em `MonthlyIncome` e `NumberOfDependents` utilizando a mediana.
   * Engenharia de atributos com a criação da variável `IncomePerPerson` (renda mensal *per capita* familiar).
4. **Transformação de Linhas:**
   * Remoção de registros duplicados.
   * Exclusão de cadastros com idade inválida (`age < 18`).
   * Filtragem de códigos de erro sistêmico (`96` e `98`) nas colunas de histórico de atrasos.
5. **Divisão Estratificada e Escalonamento:** Separação dos dados em **70% Treinamento**, **15% Validação** e **15% Teste**, com padronização de escala via `RobustScaler` ajustado exclusivamente no conjunto de treino.
6. **Modelagem e Avaliação:** Treinamento de um classificador `RandomForestClassifier` com balanceamento de classes (`class_weight='balanced'`), validação preliminar e avaliação final no conjunto de teste (**81,12% de acurácia** e **73% de recall** na detecção de inadimplentes), acompanhada da Matriz de Confusão.
7. **Simulação de Inferência:** Teste de predição simulando a entrada de um novo cliente em produção.

---

## Como Reproduzir a Execução

### Pré-requisitos
* Python 3.9 ou superior instalado
* Conta no Kaggle (caso o `kagglehub` solicite autenticação local na primeira execução)

### Passo a passo

1. **Clone este repositório:**
   ```bash
   git clone https://github.com/LeticiaSanttos/esteira-ml-risco-credito.git
   cd esteira-ml-risco-credito