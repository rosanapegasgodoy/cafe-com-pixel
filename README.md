# ☕ Café com Pixel

Experimentos semanais juntando café e visão computacional.

## Semana 1 — Classificação de torra de café

Um classificador de nível de torra (verde, clara, média, escura) a partir de fotos de grãos, comparando três abordagens:

1. **Teachable Machine** — sem código
2. **Modelo treinado** — ResNet34 pré-treinada, ajustada com [fast.ai](https://docs.fast.ai) (*transfer learning*)
3. **Modelo multimodal genérico** — Claude, só com instrução em texto, sem treino

📓 Notebook: [`semana1_torra_cafe_vscode.ipynb`](semana1_torra_cafe_vscode.ipynb)

### Base de dados

[*Coffee Bean Dataset Resized (224×224)*](https://www.kaggle.com/datasets/gpiosenka/coffee-bean-dataset-resized-224-x-224), Kaggle — 1.600 imagens de arábica, 400 por classe (300 treino + 100 teste). Licença CC BY-SA 4.0.

### Resultados — modelo treinado (fast.ai)

| Conjunto | Imagens | Acurácia | Erros |
|---|---|---|---|
| Validação (20% do treino) | 240 | 99,6% | 1 (Dark → Medium) |
| **Teste cego** | **400** | **99,8%** | 1 (Medium → Dark) |

- Treino: 3 épocas em GPU T4 (Google Colab), ~28 segundos.
- Aumento de dados com giros e espelhamentos, **sem alterar brilho/contraste**, para não confundir os níveis de torra.
- Limitação: fotos com fundo branco, luz controlada e um único tipo de café. O resultado vale para essa base, não para fotos em condições reais.

## Semana 2 — Precisava treinar? fast.ai × Teachable Machine × Claude

As três abordagens classificam **as mesmas 40 fotos** do teste (10 por torra), comparadas em acurácia, tempo por imagem, custo por 1.000 imagens e esforço. O Claude não recebe nenhum treino: só a foto e uma instrução em texto, com a resposta restrita aos 4 rótulos.

📓 Notebook: [`semana2_comparacao_tm_claude.ipynb`](semana2_comparacao_tm_claude.ipynb) — resultados em breve.

Para rodar a parte do Teachable Machine, exporte o modelo em *TensorFlow Lite → Ponto flutuante* (instruções na seção 3 do notebook).

### Como rodar

O notebook foi feito para rodar no **Google Colab com GPU T4**:

- **No VS Code:** extensão *Google Colab* → *Select Kernel* → *Colab* → *New Colab Server* → *GPU T4*.
- **No navegador:** faça upload do notebook em [colab.research.google.com](https://colab.research.google.com) → *Ambiente de execução* → *Alterar o tipo de ambiente de execução* → *T4 GPU*.

Rode as células em ordem. A seção 6 (Claude) pede uma chave da API da Anthropic, digitada na hora e não gravada no arquivo.
