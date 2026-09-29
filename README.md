# Projeto Machine Learning — Predição de Preço de Imóveis

Pipeline reprodutível que treina e compara dois modelos clássicos de regressão para prever o preço de imóveis:

- **Modelo A:** Regressão Linear Múltipla
- **Modelo B:** KNN de Regressão
- **Alvo:** `price`
- **Dataset:** `house_price_50k.csv`

O pipeline está disponível em **dois formatos equivalentes**:

- `projeto_machine.py` — script Python para rodar direto no terminal.
- `projeto_machine.ipynb` — notebook Jupyter para rodar célula por célula (ideal para visualizar gráficos e tabelas inline).

---

## 1. Estrutura do repositório

```
machine_learning/
├── projeto_machine.py      # Pipeline em script
├── projeto_machine.ipynb   # Pipeline em notebook Jupyter
├── house_price_50k.csv     # Dataset 
├── requirements.txt        # Dependências com versões fixadas
└── README.md               # Este arquivo
```

---

## 2. Requisitos

- **Conda** (recomendado): instale o [Miniconda](https://docs.conda.io/en/latest/miniconda.html) ou o [Anaconda](https://www.anaconda.com/download).
- **Python:** 3.10
- **Sistema:** Windows, Linux ou macOS
- **Bibliotecas:** listadas em `requirements.txt`

Conteúdo do `requirements.txt` 

```
numpy==1.26.4
pandas==2.2.2
matplotlib==3.8.4
scikit-learn==1.4.2
jupyter==1.0.0
```

---

## 3. Como obter o dataset

O arquivo `house_price_50k.csv` deve estar na **mesma pasta** do script/notebook.

Se o dataset não estiver no repositório (por tamanho ou licença), coloque-o manualmente nesse diretório antes de executar o pipeline.

https://www.kaggle.com/datasets/miadul/house-price-prediction-dataset

---

## 4. Preparação do ambiente (comum aos dois formatos)

### 4.1. Clonar o repositório

```bash
git clone <URL_DO_REPOSITORIO>
cd machine_learning
```

### 4.2. Criar e ativar o ambiente Conda

```bash
conda create -n machine_learning python=3.10 -y
conda activate machine_learning
```

### 4.3. Instalar as dependências

```bash
pip install -r requirements.txt
```

> Alternativa 100% conda:
> ```bash
> conda install -c conda-forge numpy=1.26.4 pandas=2.2.2 matplotlib=3.8.4 scikit-learn=1.4.2 jupyter=1.0.0 -y
> ```

---

## 5. Executando o pipeline

Escolha **uma** das duas opções abaixo.

### 5.A. Rodando o script `.py` no terminal

```bash
python projeto_machine.py
```

- As saídas de texto (métricas, tabelas) aparecem no terminal.
- Os gráficos abrem em janelas separadas do Matplotlib. Feche cada janela para continuar a execução.
- Se estiver em um ambiente sem tela (servidor), os gráficos não abrirão; nesse caso use o notebook.

### 5.B. Rodando o notebook `.ipynb` no Jupyter

Com o ambiente Conda ativo:

```bash
jupyter notebook projeto_machine.ipynb
```

Ou, se preferir o Jupyter Lab:

```bash
jupyter lab projeto_machine.ipynb
```

Também é possível abrir o `.ipynb` diretamente no **VS Code** (extensão *Jupyter*) ou no **Google Colab**.

Dentro do notebook:

1. Selecione o kernel `Python 3 (machine_learning)` (o ambiente Conda que você criou).
2. Rode as células em ordem (`Shift+Enter`) ou use *Run All*.
3. Tabelas (`DataFrame`) e gráficos são renderizados inline em cada célula.


---

## 6. O que o pipeline faz (etapas)

1. **Importa bibliotecas** e define `random_seed = 42` (garante reprodutibilidade).
2. **Carrega os dados** de `house_price_50k.csv`.
3. **EDA (Análise Exploratória):** shape, `info()`, `describe()`, valores ausentes.
4. **Diagnóstico de outliers** via IQR para todas as colunas numéricas.
5. **Balanceamento de classes** para `location` e `income_level` (tabelas + gráficos).
6. **Histograma** da variável alvo `price`.
7. **Pré-processamento:**
   - Codificação ordinal de `location` (`low < medium < premium`) e `income_level` (`low < mid < high`).
   - Split treino/teste 80/20 com `random_state=42`.
   - Padronização com `StandardScaler` (fit somente no treino).
8. **Modelo A — Regressão Linear Múltipla:** treino, previsão, métricas (MAE, MSE, RMSE, R²) e gráfico de importância dos coeficientes.
9. **Modelo B — KNN de Regressão:** busca do melhor `k` (ímpares de 1 a 99) com **early stopping** após 5 iterações sem melhora no R².
10. **Comparação** dos modelos em tabela e no gráfico Real vs Previsto.

---

## 7. Garantias de reprodutibilidade

- **Seed fixa** (`random_seed = 42`) em todo split aleatório.
- **Versões de bibliotecas fixadas** em `requirements.txt`.
- **Ordem determinística** das categorias ordinais.
- **Ambiente Conda isolado** evita conflitos com pacotes globais.
- Executando com o mesmo dataset e o mesmo `requirements.txt`, **as métricas finais devem ser idênticas** — tanto no `.py` quanto no `.ipynb`.

---


