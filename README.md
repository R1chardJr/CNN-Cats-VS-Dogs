# Classificação de Imagens: Gatos vs. Cachorros com Redes Neurais

Este projeto explora e compara diferentes arquiteturas de redes neurais para a tarefa de classificação de imagens, distinguindo entre gatos e cachorros. A análise parte de um modelo simples (MLP) como linha de base, avança para Redes Neurais Convolucionais (CNNs) customizadas e culmina no uso de técnicas de *Transfer Learning* com os modelos VGG16 e MobileNetV2.

## 📝 Descrição do Projeto

O objetivo principal é demonstrar a eficácia das Redes Neurais Convolucionais (CNNs) em tarefas de visão computacional em comparação com uma Rede Neural Multilayer Perceptron (MLP) tradicional. O notebook detalha cada passo, desde a preparação dos dados até o treinamento e a comparação final de desempenho entre os modelos.

## 💿 Dataset

O projeto utiliza o dataset "Cats and Dogs" da Microsoft, disponibilizado publicamente pelo Kaggle. O conjunto de dados contém 25.000 imagens (12.500 de cada classe).

O notebook automatiza as seguintes etapas de preparação:
1.  **Download:** Baixa o arquivo `.zip` diretamente da fonte.
2.  **Organização:** Descompacta e estrutura os arquivos em diretórios de `treino` (80%) e `validacao` (20%), mantendo as classes (gatos/caes) separadas.
3.  **Limpeza de Dados:** Arquivos corrompidos ou inválidos são identificados e removidos do conjunto de dados para garantir que o treinamento ocorra sem interrupções.

## 🛠️ Estrutura do Projeto

O fluxo de trabalho no notebook `CNNS.ipynb` está organizado da seguinte forma:

1.  **Preparação do Ambiente:** Importação das bibliotecas necessárias, como TensorFlow, Keras, NumPy, e Matplotlib.
2.  **Criação do Dataset:** Download, extração e organização do conjunto de dados de imagens.
3.  **Limpeza e Pipeline de Dados:** Verificação de integridade das imagens com TensorFlow e criação de um pipeline de dados eficiente com `tf.data` para alimentar os modelos durante o treinamento.
4.  **Modelagem e Treinamento:**
    * **Rede MLP (Baseline):** Uma rede neural densa simples é criada e treinada para estabelecer uma acurácia de base.
    * **CNNs Customizadas:** Quatro arquiteturas de CNNs são construídas e treinadas, variando o tamanho do kernel (3x3 vs. 5x5) e a profundidade da rede para analisar o impacto dessas mudanças.
    * **Transfer Learning (VGG16 e MobileNetV2):** Dois modelos pré-treinados famosos são utilizados como extratores de características. Suas camadas convolucionais são "congeladas" e novas camadas de classificação são adicionadas e treinadas com os dados do projeto.
5.  **Análise Comparativa:** Os resultados de acurácia, número de parâmetros e a matriz de confusão dos modelos mais performáticos são comparados para extrair conclusões.

## 🚀 Modelos Desenvolvidos

-   **MLP (Baseline):** Uma rede com uma camada de achatamento (`Flatten`) seguida por duas camadas densas (`Dense`). Serviu para mostrar as limitações de uma abordagem que não considera a estrutura espacial das imagens.
-   **CNN 1 e 3 (Kernel 3x3):** Redes convolucionais com 3 e 4 camadas `Conv2D`, respectivamente, usando filtros de tamanho 3x3.
-   **CNN 2 e 4 (Kernel 5x5):** Arquiteturas similares às anteriores, mas com filtros de 5x5 para capturar padrões espaciais maiores.
-   **Transfer Learning com VGG16:** Utiliza a base convolucional do modelo VGG16, conhecido por sua profundidade e eficácia, mas com um alto número de parâmetros.
-   **Transfer Learning com MobileNetV2:** Utiliza a base do MobileNetV2, uma arquitetura otimizada para eficiência, com significativamente menos parâmetros.

## 📊 Resultados

A comparação final demonstrou a clara superioridade das abordagens baseadas em convoluções para o problema.

| Modelo                          | Acurácia de Validação | Parâmetros Treináveis |
| :------------------------------ | :-------------------- | :-------------------- |
| MLP (Baseline)                  | ~63.4%                | 6,299,905             |
| CNN (Customizada - 5x5)         | ~84.5%                | 456,705               |
| VGG16 (Transfer Learning)       | ~88.8%                | 131,585               |
| **MobileNetV2 (Transfer Learning)** | **~97.0%** | **328,193** |

### Conclusão
-   A **MLP** teve o pior desempenho e o maior número de parâmetros, pois ao "achatar" a imagem, perde toda a informação espacial, que é crucial para a análise.
-   As **CNNs customizadas** superaram a MLP com folga e com muito menos parâmetros, provando a eficiência das camadas convolucionais. O kernel 5x5 se mostrou ligeiramente superior para este problema.
-   O **Transfer Learning** obteve os melhores resultados. O **MobileNetV2** foi o grande destaque, alcançando a maior acurácia (**~97%**) com um número de parâmetros significativamente menor que o da MLP, demonstrando ser um modelo extremamente eficiente e poderoso.

## Como Executar

1.  **Ambiente:** O notebook foi desenvolvido para ser executado em ambientes como Google Colab ou Jupyter Notebook com GPU.
2.  **Dependências:** Certifique-se de ter as principais bibliotecas instaladas:
    ```bash
    pip install tensorflow numpy pandas matplotlib seaborn scikit-learn
    ```
3.  **Execução:** Abra o arquivo `CNNS.ipynb` e execute as células em ordem sequencial. O download e a preparação dos dados são feitos automaticamente pelo código.
