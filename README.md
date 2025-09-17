# 📦 Importação das Bibliotecas  

Nesta etapa inicial, são importadas todas as bibliotecas necessárias para o **pré-processamento de dados, análise estatística, visualização gráfica e modelagem preditiva**.  

---

## 🔧 Principais bibliotecas utilizadas  

- **Manipulação e análise de dados**  
  - `numpy` → Operações matemáticas e vetoriais  
  - `pandas` → Estruturação e manipulação de *datasets*  

- **Visualização de dados**  
  - `matplotlib.pyplot` → Gráficos básicos e personalizáveis  
  - `seaborn` → Visualizações estatísticas com estilo aprimorado  

- **Pré-processamento**  
  - `StandardScaler` → Normalização dos dados  
  - `LabelEncoder` → Codificação de variáveis categóricas  

- **Redução de dimensionalidade**  
  - `PCA` (*Principal Component Analysis*) → Extração de componentes principais  

- **Seleção de características**  
  - `RFE` (*Recursive Feature Elimination*) → Seleção de atributos relevantes  

- **Modelos de aprendizado de máquina**  
  - `LogisticRegression` → Classificação linear  
  - `Lasso` → Regressão com regularização L1  
  - `RandomForestClassifier` → Modelo de ensemble baseado em árvores de decisão  

- **Validação e métricas**  
  - `train_test_split`, `cross_val_score` → Divisão de dados e validação cruzada  
  - `accuracy_score`, `classification_report` → Avaliação de desempenho  

- **Outros recursos**  
  - `warnings` → Controle de mensagens de alerta  

---

## 🎨 Configurações de visualização  

- Tamanho padrão das figuras ajustado para **12x8**  
- Estilo gráfico definido como `default`  
- Paleta de cores `husl` aplicada no Seaborn  

---

✅ **Mensagem de verificação**:  
```python
print("Bibliotecas importadas com sucesso!")

## 📂 Carregamento dos Dados

Nesta célula, os caminhos do **dataset** são definidos e os arquivos são carregados do Google Drive.  
Foram utilizados os seguintes arquivos:  

- `X_train.txt` → atributos de treino  
- `y_train.txt` → rótulos de treino  
- `X_test.txt` → atributos de teste  
- `y_test.txt` → rótulos de teste  
- `features.txt` → nomes das variáveis  
- `activity_labels.txt` → mapeamento das atividades  

Ao final, são exibidos os **shapes** de cada conjunto para confirmar o carregamento correto.  


## 🔄 Combinação e Identificação dos Dados

Nesta etapa:  
- Foram **unidos** os conjuntos de treino e teste em `X` (atributos) e `y` (rótulos).  
- As colunas de `X` receberam nomes genéricos (`feature_0`, `feature_1`, ...).  
- O vetor `y` ganhou o mapeamento das atividades para nomes descritivos:
  - WALKING  
  - WALKING_UPSTAIRS  
  - WALKING_DOWNSTAIRS  
  - SITTING  
  - STANDING  
  - LAYING  

Também foram exibidas informações gerais:  
- Número total de amostras  
- Número de atributos  
- Número de classes distintas  
- Distribuição de amostras por classe  

Por fim, foi feita a **verificação de valores faltantes** em `X` e `y`.  


## ⚙️ Pré-processamento dos Dados

Nesta etapa:  
- Foram separados os **atributos (`X_data`)** e os **rótulos (`y_data`)**.  
- Aplicou-se a **normalização com StandardScaler**, fundamental para métodos como PCA.  

Resultados exibidos:  
- Média e desvio padrão antes da normalização.  
- Média e desvio padrão após normalização (esperados ≈ 0 e ≈ 1).  
- Estatísticas de algumas features para verificar a padronização.  


## 📊 PCA com 2 Componentes

Nesta etapa foi aplicado o **PCA (Principal Component Analysis)** para reduzir os dados a **2 componentes principais**.  

Informações exibidas:  
- Variância explicada por cada componente (PC1 e PC2).  
- Variância total explicada pelos dois componentes.  

Também foi gerado um **gráfico de dispersão em 2D**, onde:  
- Cada ponto representa uma amostra do dataset.  
- As cores diferenciam as atividades (`WALKING`, `SITTING`, `STANDING`, etc.).  
- Os eixos PC1 e PC2 indicam a proporção de variância capturada.  


## 📈 PCA com Todos os Componentes

Nesta etapa, o **PCA foi aplicado sem restrição do número de componentes**, permitindo analisar a contribuição de cada um deles.  

### 🔎 Objetivos
- Calcular a **variância explicada individualmente** por cada componente.  
- Obter a **variância acumulada**, que indica a proporção total de informação retida à medida que novos componentes são adicionados.  
- Determinar o número mínimo de componentes necessários para reter **90% da variância**.  

### ✅ Resultados
- O número de componentes necessário para atingir 90% da variância foi identificado (`n_components_90`).  
- A variância acumulada correspondente foi exibida.  

### 📊 Visualização
Foram construídos dois gráficos complementares (*scree plots*):  
1. **Variância explicada individual** pelos primeiros 50 componentes.  
2. **Variância acumulada** até 100 componentes, destacando a linha de corte de 90% e o ponto exato onde ela é alcançada.  

Essas visualizações permitem observar:  
- Quais componentes carregam mais informação.  
- Em que ponto adicionar novos componentes deixa de trazer ganhos significativos.  


## 🔍 RFE - Recursive Feature Elimination (Simplificado)

Nesta etapa foi aplicada a técnica de **RFE (Recursive Feature Elimination)** para seleção de atributos mais relevantes.  

### ✔️ Procedimentos
- Divisão dos dados em treino (80%) e teste (20%) com estratificação.  
- Classificadores utilizados:  
  - **Logistic Regression**  
  - **Random Forest** (versão leve, `n_estimators=20`)  
- Testados diferentes números de atributos selecionados: **10, 30 e 50**.  
- Acurácias obtidas para cada caso foram registradas e comparadas em gráfico.  

### 📊 Resultados
- O gráfico mostra a relação entre **número de features** e **acurácia** para cada classificador.  
- Também foram identificadas as **features mais relevantes** usando **Random Forest + RFE (30 atributos)**.  

Esse processo ajuda a verificar se é possível manter boa performance do modelo com um conjunto reduzido de variáveis.  


## 🏹 Lasso - Regularização L1

Nesta etapa foi aplicada a **regularização L1 (Lasso)** usando `LogisticRegression` para o problema multiclasse.  

### ✔️ Procedimentos
- Testados diferentes valores de **C** (inverso da regularização): `0.001, 0.01, 0.1, 1, 10`.  
- Para cada valor de C foram avaliados:  
  - **Acurácia** no conjunto de teste.  
  - **Número de features não-zero** (selecionadas pelo Lasso).  
- Identificado o **melhor valor de C** com base na maior acurácia.  

### 📊 Resultados exibidos
1. **Número de features não-zero vs C** → mostra como o nível de regularização afeta a seleção.  
2. **Acurácia vs C** → permite observar a performance em relação à força da penalização.  
3. **Coeficientes não-zero do melhor modelo** → destaca quais atributos foram mantidos.  

### ✅ Conclusão
- O melhor valor de **C** foi exibido, junto com sua acurácia e número de features selecionadas.  
- Também foi listada a quantidade total de atributos escolhidos e os índices das **primeiras 20 features relevantes**.  


## 🔄 Comparação RFE vs Lasso

Nesta etapa, comparamos os atributos selecionados pelos dois métodos de **seleção de features**:  
- **RFE (Recursive Feature Elimination)**  
- **Lasso (Regularização L1)**  

### ✔️ Métricas calculadas
- Número total de features selecionadas por cada método.  
- Número de features em comum.  
- Features únicas de cada método.  
- Percentual de sobreposição entre RFE e Lasso.  

### 📊 Visualizações
1. **Diagrama de Venn aproximado** → mostra graficamente as features únicas e comuns.  
2. **Gráfico de barras comparativo** → quantifica o número de features selecionadas por cada método e as compartilhadas.  

Essas análises ajudam a entender **semelhanças e diferenças na seleção de atributos**, indicando quais variáveis são mais consistentes entre métodos.  


## 🔎 Análise de Padrões e Tendências

### 1️⃣ Separabilidade no PCA
- Apenas 2 componentes explicam **~{total_variance_2d*100:.2f}%** da variância total.  
- Atividades estáticas (SITTING, STANDING, LAYING) tendem a se agrupar.  
- Atividades dinâmicas (WALKING variants) formam clusters distintos.  
- Sobreposição entre algumas classes indica que **2 componentes não são suficientes** para separação completa.

### 2️⃣ Comparação RFE vs Lasso
- **Taxa de concordância**: {overlap_ratio*100:.1f}%  
- Alta concordância → métodos identificam features similares.  
- Média/baixa concordância → diferenças importantes entre os métodos.

### 3️⃣ Benefícios e limitações dos métodos
**PCA:**  
+ Reduz dimensionalidade e preserva variância  
- Perde interpretabilidade  

**RFE:**  
+ Mantém interpretabilidade, considera importância para classificação  
- Computacionalmente mais caro, depende do classificador base  

**Lasso:**  
+ Seleção automática, previne overfitting, eficiente  
- Pode remover features correlacionadas, sensível à escala dos dados

---

## 🏁 Resumo Final dos Resultados

**Dataset UCI HAR:**  
- Amostras: {n_samples}  
- Features: {n_features}  
- Classes: {n_classes}  

**PCA:**  
- 2 componentes explicam ~{total_variance_2d*100:.2f}% da variância  
- Para 90% da variância: {n_components_90} componentes  

**RFE (Random Forest):**  
- Melhor performance com ~100-150 features  
- Features selecionadas: {len(selected_features_rfe)}  

**Lasso:**  
- Melhor C: {best_C}  
- Features selecionadas: {len(features_selected_lasso)}  
- Acurácia: {best_lasso['accuracy']:.4f}  

**Comparação RFE vs Lasso:**  
- Features em comum: {len(common_features)}  
- Taxa de concordância: {overlap_ratio*100:.1f}%  

**Conclusão:**  
- O dataset UCI HAR possui alta dimensionalidade que pode ser reduzida eficazmente.  
- PCA é ideal para visualização; RFE e Lasso preservam interpretabilidade e performance de classificação.  
- A escolha do método depende do objetivo: visualização (PCA) vs interpretabilidade e classificação (RFE/Lasso).

---

### 💾 Resultados Salvos
Os principais resultados foram armazenados em `results_summary` para futuras análises ou relatórios.




