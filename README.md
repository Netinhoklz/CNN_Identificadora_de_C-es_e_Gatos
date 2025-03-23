# Projeto de Classificação de Imagens de Gatos e Cachorros com CNN

Este repositório contém um projeto desenvolvido para classificar imagens de gatos e cachorros utilizando uma rede neural convolucional (CNN). O código, originalmente gerado pelo Google Colab, passa por diversas etapas de processamento, modelagem e análise de resultados, detalhadas a seguir de forma resumida.

## 1. Configuração e Importação de Bibliotecas

- **Importações iniciais:**  
  São importadas bibliotecas essenciais para manipulação de dados (`pandas`, `numpy`), visualização (`matplotlib`, `seaborn`), processamento de imagens (`cv2` e `zipfile`) e construção de modelos com TensorFlow/Keras.
  
- **Download e extração dos dados:**  
  Utilizou-se o comando `!gdown` para baixar um arquivo compactado que contém as imagens, seguido de uma extração do conteúdo com a biblioteca `zipfile`.

## 2. Conhecendo o Dataset

- **Descrição do Dataset:**  
  O dataset possui 697 imagens de gatos e cachorros com resoluções variadas, o que exige um redimensionamento das imagens para um tamanho padrão durante o pré-processamento.
  
- **Visualização:**  
  São exibidas amostras das imagens, onde é feito o redimensionamento e a conversão de cores (de BGR para RGB) para garantir a correta visualização.

## 3. Pré-processamento dos Dados

- **Função `load_images`:**  
  Esta função percorre uma pasta com imagens, realiza os seguintes passos:
  - Leitura da imagem com OpenCV.
  - Conversão para escala de cinza.
  - Redimensionamento para um tamanho definido (padrão 100x100 pixels).
  - Normalização dos valores dos pixels (dividindo por 255.0).

- **Organização dos dados:**  
  As imagens são carregadas separadamente para gatos e cachorros, tanto para os conjuntos de treino quanto para teste. Em seguida, os dados são concatenados e divididos em conjuntos de treino, validação e teste utilizando `train_test_split` com estratificação, garantindo a proporcionalidade das classes.

## 4. Construção do Modelo CNN

- **Arquitetura do Modelo:**
  - **Blocos Convolucionais:**  
    São utilizados três blocos, cada um composto por uma camada de `Conv2D` seguida de uma camada de `MaxPooling2D` para extração progressiva de características das imagens.
  
  - **Camadas Densas:**  
    Após a etapa convolucional, o modelo é achatado com `Flatten` e passa por várias camadas densas (`Dense`), intercaladas com camadas de `Dropout` para reduzir overfitting.
  
  - **Saída:**  
    A camada final possui uma única unidade com ativação `sigmoid`, ideal para problemas de classificação binária (gato vs. cachorro).

## 5. Compilação e Treinamento do Modelo

- **Compilação:**  
  O modelo é compilado utilizando o otimizador Adam com um *learning rate* ajustado manualmente para `0.00001`, e a função de perda `binary_crossentropy` é utilizada, juntamente com a métrica de `accuracy`.

- **Treinamento:**  
  Durante o treinamento, é implementado um *EarlyStopping* que monitora a acurácia de validação e interrompe o treinamento automaticamente se não houver melhoria após 20 épocas. O treinamento está configurado para até 100 épocas, otimizando o modelo para evitar o overfitting.

## 6. Análise dos Resultados

- **Relatório de Classificação:**  
  Após o treinamento, o modelo é avaliado utilizando o conjunto de teste. São geradas métricas como precisão, recall e F1-score para cada classe (gato e cachorro).

- **Visualização dos Desempenhos:**  
  - **Curvas de Acurácia e Loss:**  
    Gráficos que mostram a evolução da acurácia e da função de perda durante o treinamento e validação.
  
  - **Matriz de Confusão:**  
    Utilizando `seaborn`, é plotada uma matriz de confusão que facilita a visualização dos acertos e erros do modelo.
  
  - **Curva ROC:**  
    A curva ROC é gerada, e a área sob a curva (AUC) é calculada, permitindo uma avaliação mais aprofundada da performance do classificador.

- **Visualização de Previsões:**  
  São exibidas imagens aleatórias do conjunto de teste com os rótulos reais e as previsões do modelo, destacando se a predição foi correta (indicada em verde) ou incorreta (em vermelho).

## Conclusão

Este projeto demonstra um pipeline completo de classificação de imagens utilizando CNNs, desde o pré-processamento dos dados até a análise detalhada dos resultados. Cada etapa foi cuidadosamente planejada para garantir a correta manipulação das imagens e a construção de um modelo robusto, capaz de distinguir entre gatos e cachorros com alta precisão.
