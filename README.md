
# 🧠 Deep Learning com Algoritmo Genético (AG) para Classificação de Dígitos Manuscritos ✍️

📌 Repositório: https://github.com/araujofran/digits-ag-dl

Este projeto 🚀 combina Deep Learning com Algoritmos Genéticos (AG) para otimizar a camada de uma Rede Neural na classificação de dígitos do dataset digits (0–9) 🔢. Nosso objetivo é explorar como o AG pode encontrar os melhores pesos para uma parte da rede, enquanto o restante aprende do jeito tradicional! ✨

---

## 🌟 Visão Geral do Projeto

- Preparação dos Dados 📊  
  Carregar, normalizar e dividir o dataset digits.  

- Arquitetura da Rede Neural 🏗️  
  Definir a MLP, escolhendo uma camada para ser otimizada pelo AG.  

- Otimização Híbrida 🧬⚙️  
  Usar AG para evoluir os pesos da camada selecionada, enquanto RMSprop ajusta o resto.  

- Avaliação e Visualização 🎯📈  
  Avaliar acurácia, visualizar evolução da aptidão e distribuição de pesos.  

---

## 📖 Como Funciona (Detalhes do Código)

### 0. Setup Inicial e Importações 🛠️
Importamos as bibliotecas essenciais: NumPy, TensorFlow/Keras, Scikit-learn, Pandas, Matplotlib e Seaborn.

### 1. Funções Base e Auxiliares 👷‍♀️
- **load_and_preprocess_data()**  
  Carrega o dataset, normaliza pixels (0–16 para 0–1) e divide treino/teste.  

- **build_model_for_ag_fitness()**  
  Constrói a MLP com:  
  - Input(shape=(64,))  
  - Camada otimizada pelo AG: `Dense(128, activation='relu')` (congelada após receber pesos do AG)  
  - `Dense(64, activation='relu')`  
  - `Dense(10, activation='softmax')`  
  Compila com `sparse_categorical_crossentropy` e `rmsprop`.  

- **flatten_weights() / unflatten_weights()**  
  Converter pesos entre lista de matrizes e vetor unidimensional.

### 2. Preparação dos Dados e Parâmetros 📝
- Carregamento e divisão, separando um hold-out para avaliação de aptidão.  
- `individual_size`: tamanho do “DNA” (pesos + vieses) que o AG vai evoluir.  
- Parâmetros do AG: população, gerações, taxa de mutação, crossover, elitismo.

### 3. Funções do Algoritmo Genético 🧬
- **generate_initial_population()**: inicia população com pesos aleatórios.  
- **evaluate_fitness()**: constrói modelo para cada indivíduo, treina outras camadas por 5 épocas e mede acurácia.  
- **select_parents()**: escolhe elites e faz torneios para selecionar pais.  
- **crossover()**: combina “DNA” de dois pais para gerar filhos.  
- **mutate()**: altera aleatoriamente alguns genes (pesos) para manter diversidade.  
- **replace_population()**: substitui gerações antigas pelas novas.

### 4. Loop Principal do AG: A Grande Evolução! 📈
Em cada geração: avalia, seleciona, cruza, muta e substitui. Registramos aptidão máxima e média para visualizar progresso.

### 5. Análise de Progresso (Visualizações) 👀
- Gráfico de Aptidão: evolução da acurácia ao longo das gerações.  
- Histogramas de Pesos: comparação entre primeira e última geração.

### 6. Avaliação Final do Modelo Híbrido 🏆
- O melhor indivíduo é fixado na rede.  
- As outras camadas fazem um treino final de 50 épocas.  
- Métricas de acurácia e perda são avaliadas no conjunto de teste.  
- Sumário em tabela dos resultados.

---

## 💪 Por Que Usar AG com Deep Learning?

- Exploração Poderosa: AGs encontram soluções em espaços complexos onde otimizadores tradicionais podem falhar.  
- Robustez: geram soluções diversas e resistentes a mínimos locais.  
- Otimização de Hiperparâmetros/Arquitetura: ideal para ajustar partes sensíveis de uma rede.  

---

## 🚀 Como Rodar o Projeto

1. Instale as bibliotecas:
   ```bash
   pip install numpy tensorflow keras scikit-learn pandas matplotlib seaborn
   ```

2. Clone o repositório e execute:
   ```bash
   git clone https://github.com/araujofran/digits-ag-dl.git
   cd digits-ag-dl
   python main.py
   ```

3. Ou abra o notebook em Jupyter/Colab.

---

## 💡 Próximos Passos (Ideias para Melhorar)

- Compare contra uma rede sem AG para medir ganhos de performance.  
- Experimente diferentes parâmetros de AG (população, gerações, taxas).  
- Otimize múltiplas camadas ou toda a arquitetura pelo AG.  
- Visualize como o AG altera as representações internas dos dados.  
```
