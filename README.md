# Árvore de Regressão para Previsão do Fator de Segurança de Taludes

<!-- Badges -->
[![DOI](https://img.shields.io/badge/DOI-repo-blue)]() <!-- REPO_DOI -->
[![DOI](https://img.shields.io/badge/DOI-dataset-orange)](https://doi.org/10.5281/zenodo.19133633)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.12](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]() <!-- COLAB_LINK -->

## Descrição

Trabalho de Conclusão de Curso (TCC) desenvolvido na Universidade Federal de Santa Catarina (UFSC), que utiliza **Árvore de Regressão** (`DecisionTreeRegressor`) para prever o **Fator de Segurança (FS)** de taludes homogêneos e secos.

O modelo substitui métodos tradicionais de equilíbrio limite por uma abordagem baseada em aprendizado de máquina, utilizando **parâmetros adimensionais** derivados das propriedades geométricas e geotécnicas do talude.

## Dados

Os dados são provenientes do Zenodo: [10.5281/zenodo.19133633](https://doi.org/10.5281/zenodo.19133633)

**Features de entrada:**

| Feature | Descrição | Fórmula |
|---------|-----------|---------|
| `ns` | Número de estabilidade | coesão / (peso_específico × altura) |
| `tan` | Razão de ângulo de atrito | tan(φ) / tan(β) |

**Target:**

| Target | Descrição |
|--------|-----------|
| `lfs` | log₁₀(FS) — fator de segurança em escala logarítmica |

A altura do talude é fixada em 3,5 m para o cálculo dos parâmetros adimensionais.

## Como Executar

### Google Colab (mais simples)

Abra o notebook diretamente no navegador, sem instalação:

<!-- COLAB_LINK -->
> Link do Colab será adicionado após publicação do repositório.

### Localmente com uv + VSCode

1. **Instale o [uv](https://docs.astral.sh/uv/):**

   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Clone o repositório:**

   ```bash
   git clone https://github.com/zipluciano/slope-stability-regression-tree.git
   cd slope-stability-regression-tree
   ```

3. **Instale as dependências** (o `uv` instala o Python 3.12.12 automaticamente):

   ```bash
   uv sync
   ```

4. **Abra no VSCode** e selecione o kernel Python do `.venv`:

   ```bash
   code .
   ```

   No VSCode, abra `regression_tree_fos.ipynb` e selecione o interpretador Python localizado em `.venv/bin/python`.

5. **Execute o notebook** célula por célula.

## Modelo

O modelo utiliza `DecisionTreeRegressor` do scikit-learn com os seguintes hiperparâmetros:

| Parâmetro | Valor |
|-----------|-------|
| `max_depth` | 7 |
| `min_samples_leaf` | 3 |
| `min_samples_split` | 5 |
| `criterion` | `squared_error` |

As previsões são transformadas de volta para a escala original via 10^valor_previsto para obter o FS real.

## Resultados

O notebook gera os seguintes resultados:

- Métricas de desempenho no conjunto de treino e teste (RMSE, MAE, R²)
- Gráfico de dispersão: FS previsto vs. FS real
- Análise de resíduos por faixa de FS
- Visualização da árvore de decisão (exportada em SVG/PDF)
- Importância das features

## Estrutura do Repositório

```
slope-stability-regression-tree/
├── regression_tree_fos.ipynb   # Notebook principal
├── pyproject.toml              # Dependências do projeto (uv)
├── .python-version             # Versão do Python (3.12.12)
├── .gitignore
├── CLAUDE.md
├── LICENSE                     # Licença MIT
└── README.md
```

## Citação

Se você utilizar este trabalho, por favor cite:

```bibtex
@software{monteiro2025slope,
  author    = {Monteiro, Luciano Espindula},
  title     = {Árvore de Regressão para Previsão do Fator de Segurança de Taludes},
  year      = {2025},
  url       = {https://github.com/zipluciano/slope-stability-regression-tree},
  note      = {Trabalho de Conclusão de Curso, UFSC}
}
```

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

## Autor

**Luciano Espindula Monteiro** — Graduando em Engenharia Civil, UFSC

**Orientadora:** Prof. Dr.-Ing. Stephanie Thiesen ([@sthiesen](https://github.com/sthiesen))
