# Diagnóstico e Diferenciação de Arboviroses (Dengue e Chikungunya) usando Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1axUa3oWJbKUiRUY3kROBg4J93Je3Ssde?usp=sharing)

Este projeto desenvolve modelos de classificação (Árvore de Decisão e KNN) para atuar como uma triagem inicial e diagnóstica para casos de suspeitas de arboviroses. Os modelos foram treinados com dados reais do DataSUS (SINAN) referentes aos anos de 2021 a 2025.

A arquitetura do projeto foi dividida em dois modelos em cascata:
* **Modelo 1 (Triagem):** Atua na triagem inicial, classificando se o paciente tem ou não uma arbovirose.
* **Modelo 2 (Diferenciação):** Dado um caso confirmado, diferencia se a arbovirose é Dengue ou Chikungunya.

## 🛠️ Tecnologias e Ferramentas
* **Linguagem e Bibliotecas:** Python, Pandas, NumPy, Matplotlib, Scikit-learn.
* **Modelos:** Decision Tree Classifier e K-Nearest Neighbors (KNN).
* **Técnicas Adicionais:** StandardScaler para normalização geométrica de distância, Amostragem Estratificada para manutenção da proporção de classes e SMOTE (Oversampling) para tratamento de desbalanceamento.

## 📊 Pipeline e Engenharia de Dados
* **Amostragem:** Extração de 20.000 amostras aleatórias por ano de cada doença, formando um dataset de 200.000 instâncias para mitigar vieses de surtos sazonais.
* **Prevenção de Data Leakage:** Remoção rigorosa de atributos referentes a exames laboratoriais (PCR, sorologia) e desfechos clínicos (internação, óbito) para garantir que o modelo utilize puramente os sintomas clínicos da triagem].
* **Tratamento de Comorbidades:** Variáveis de histórico prévio foram excluídas no Modelo 1 e mantidas no Modelo 2, validando a literatura médica de que comorbidades influenciam a diferenciação viral.
* **Engenharia de Atributos:** Binarização de sintomas categóricos, conversão da codificação de idades do SINAN para anos inteiros e condensação de dezenas de sinais de alarme/gravidade em features booleanas otimizadas.

## 💡 Análise de Resultados e Explicabilidade
O uso da Árvore de Decisão permitiu uma auditoria clínica da estrutura de regras gerada, garantindo alta explicabilidade geométrica:

* **Modelo 1 (Triagem - Acurácia: 0,73):** A explicabilidade revelou que o modelo apoiou-se em um viés temporal (sazonalidade) para realizar previsões devido à ausência de atributos sobre sintomas respiratórios nos dados do SINAN, prejudicando a identificação de verdadeiros negativos.
* **Modelo 2 (Diferenciação - Acurácia: 0,80 / F1-Score: 0,78):** Apresentou alta coesão biomédica. O modelo elegeu de forma autônoma a presença de **artralgia** (dor nas articulações) como nó raiz, validando matematicamente o consenso médico de que este é o principal divisor clínico entre Dengue e Chikungunya.

## 🚀 Como Executar
Você pode rodar o modelo diretamente no navegador clicando no botão **Open in Colab** no topo desta página.

Caso queira executar localmente:
1. Clone este repositório.
2. Certifique-se de instalar as dependências (`pip install pandas numpy scikit-learn matplotlib`).
3. Execute o script ou notebook `ModeloArbovirose.ipynb` para treinar os modelos e plotar a Matriz de Confusão e a Árvore de Decisão.

📄 *Para uma análise aprofundada dos resultados, consulte o relatório técnico em PDF disponível neste repositório.*
