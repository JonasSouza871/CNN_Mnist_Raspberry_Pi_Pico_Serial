# Projeto CNN MNIST TinyML

<div align="center">

[![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![Raspberry Pi Pico](https://img.shields.io/badge/Raspberry%20Pi%20Pico-B0BD00?style=for-the-badge&logo=Raspberry-Pi&logoColor=white)](https://www.raspberrypi.com/products/raspberry-pi-pico/)
[![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))

</div>

## Visão Geral

Este projeto implementa uma Rede Neural Convolucional (CNN) para reconhecimento de dígitos manuscritos usando o dataset MNIST, especificamente otimizado para implantação em microcontroladores como o Raspberry Pi Pico. O modelo é treinado usando TensorFlow e convertido para o formato TensorFlow Lite (TFLite) com quantização INT8 para execução eficiente em dispositivos com recursos limitados.

## Recursos

- **Arquitetura CNN Leve**: Projetada especificamente para aplicações TinyML
- **Conversão TFLite**: Quantização INT8 otimizada para implantação em microcontroladores
- **Pipeline Completo de Treinamento**: Desde o pré-processamento dos dados até a avaliação do modelo
- **Métricas de Desempenho**: Avaliação abrangente com acurácia, matriz de confusão e relatórios de classificação
- **Pronto para Hardware**: Pronto para implantação no Raspberry Pi Pico e microcontroladores semelhantes

## Estrutura do Repositório

```
cnn_mnist_tinyML/
├── notebooks/                 # Notebooks Jupyter para treinamento
│   └── Model_Training.ipynb   # Notebook principal de treinamento
├── firmware/                  # Firmware do microcontrolador
│   ├── cnn_mnist.c            # Código principal de inferência
│   ├── tflm_wrapper.cpp       # Wrapper TensorFlow Lite Micro
│   └── tflm_wrapper.h         # Arquivo de cabeçalho para TFLM
├── models/                    # Modelos treinados (formato TFLite)
├── Images/                    # Gráficos e visualizações geradas
├── test/                      # Dados e amostras de teste
├── pico-tflmicro/             # Biblioteca TensorFlow Lite Micro
├── build/                     # Artefatos de compilação
├── README.md                  # Este arquivo
└── CMakeLists.txt             # Configuração de compilação
```

### Notebooks

Contém o notebook de treinamento principal com implementação abrangente:

- **Pré-processamento de Dados**: Carregamento e preparação do dataset MNIST
- **Arquitetura do Modelo**: Design CNN leve otimizado para TinyML
- **Processo de Treinamento**: Treinamento completo com validação
- **Avaliação**: Métricas de desempenho e visualizações
- **Conversão do Modelo**: Conversão TFLite com quantização INT8

<div align="center">
<img src="Images/sample_images.png" alt="Imagens de Exemplo MNIST" width="600"/>
<p><em>Amostras de imagens MNIST usadas para treinamento</em></p>
</div>

### Firmware

Implementação do lado do microcontrolador:

- **Inferência CNN**: Motor de inferência eficiente para microcontroladores
- **Wrapper TFLM**: Interface com TensorFlow Lite Micro
- **Comunicação Serial**: Transferência de dados e relatório de resultados

### Modelos

Contém os modelos TFLite convertidos:

- **Modelos Quantizados**: Quantização INT8 para execução eficiente
- **Arquivos de Cabeçalho**: Arquivos compatíveis com C para incorporação
- **Otimizado para Tamanho**: Pegada de memória mínima para microcontroladores

<div align="center">
<img src="Images/training_validation_curves.png" alt="Curvas de Treinamento" width="600"/>
<p><em>Curvas de treinamento e validação mostrando o desempenho do modelo</em></p>
</div>

### Imagens

Visualizações geradas a partir do processo de treinamento:

- **Imagens de Exemplo**: Visualização das amostras do dataset MNIST
- **Curvas de Treinamento**: Acurácia e perda ao longo das épocas
- **Matriz de Confusão**: Análise detalhada de desempenho
- **Resultados de Validação**: Previsões do modelo em amostras de teste

<div align="center">
<img src="Images/confusion_matrix.png" alt="Matriz de Confusão" width="600"/>
<p><em>Matriz de confusão mostrando o desempenho do modelo em todas as classes de dígitos</em></p>
</div>

### Teste

Arquivos de dados e validação:

- **Amostras de Teste**: Dados pré-processados para validação
- **Scripts de Validação**: Scripts para verificar o desempenho do modelo
- **Benchmarks de Desempenho**: Métricas de comparação

### Sistema de Compilação

- **Integração CMake**: Sistema de compilação multiplataforma
- **SDK Pico**: Integração com Raspberry Pi Pico SDK
- **Integração TFLM**: TensorFlow Lite Micro integração

## Arquitetura

### Arquitetura do Modelo
```
Entrada (28x28x1)
    ↓
Conv2D (8 filtros, 3x3, stride=2) → 14x14x8
    ↓
Conv2D (16 filtros, 3x3, stride=2) → 7x7x16
    ↓
Global Average Pooling → 16
    ↓
Dense (10 unidades, softmax) → 10 (classes de dígitos)
```

### Recursos Principais
- **Parâmetros Totais**: ~1.418 (menos de 6KB)
- **Quantização**: INT8 para eficiência de memória
- **Camadas**: 4 camadas (2 conv + 1 pooling + 1 dense)
- **Operações**: Otimizado para execução em microcontroladores

## Começando

### Pré-requisitos
- Python 3.7+
- TensorFlow 2.x
- Jupyter Notebook
- Raspberry Pi Pico SDK (para implantação em hardware)

### Treinando o Modelo
1. Navegue até o diretório `notebooks/`
2. Abra `Model_Training.ipynb`
3. Execute todas as células para treinar e converter o modelo

### Implantando no Hardware
1. Converta o modelo para formato de cabeçalho
2. Copie para o diretório `firmware/`
3. Compile usando CMake com Pico SDK
4. Faça flash para o Raspberry Pi Pico

## Desempenho

- **Acurácia de Treinamento**: ~89%
- **Acurácia de Validação**: ~88%
- **Acurácia de Teste**: ~88.8%
- **Tamanho do Modelo**: ~5KB (quantizado INT8)
- **Tempo de Inferência**: < 10ms no Pico

## Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para submeter pull requests ou abrir issues para bugs e solicitações de recursos.

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo LICENSE para detalhes.

## Agradecimentos

- [TensorFlow Lite Micro](https://www.tensorflow.org/lite/microcontrollers) por possibilitar ML em microcontroladores
- [Dataset MNIST](http://yann.lecun.com/exdb/mnist/) para o dataset de dígitos manuscritos
- [Fundação Raspberry Pi](https://www.raspberrypi.org/) pela plataforma Pico