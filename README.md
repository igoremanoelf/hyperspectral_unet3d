# 🌍 Hyperspectral Gas Leak Detection with 3D U-Net

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-red)
![Status](https://img.shields.io/badge/Status-Research%20Complete-success)

> **Detecção de anomalias atmosféricas (metano/poluentes) utilizando Deep Learning em Cubos de Dados Hiperespectrais.**

## 📖 Sobre o Projeto

A detecção de vazamentos de gases invisíveis a olho nu (como Metano - $CH_4$) é um desafio crítico para a indústria de energia e monitoramento ambiental. Câmeras RGB convencionais não capturam essas assinaturas.

Este projeto implementa uma pipeline completa de Visão Computacional Hiperespectral (HSI) que processa cubos de dados tridimensionais $(H \times W \times \lambda)$ para realizar segmentação semântica de alta precisão.

O modelo final atingiu um **IoU de 98.8%** na identificação de anomalias espectrais, superando abordagens tradicionais de classificação pixel-a-pixel.

## 🧠 Arquitetura e Metodologia

O diferencial deste projeto é o tratamento volumétrico dos dados, preservando a correlação físico-química entre as bandas espectrais.

1.  **Engenharia de Dados:**
    * Correção Atmosférica e Leitura de Cubos HSI.
    * **PCA (Principal Component Analysis):** Redução de dimensionalidade de 200 para 15 bandas principais, preservando 99% da variância espectral.
    * **Data Augmentation 4D:** Rotações e espelhamentos volumétricos para combater a escassez de dados.

2.  **Modelo: 3D U-Net Espaço-Espectral:**
    * Substituição de convoluções 2D por **Convoluções 3D**.
    * Encoder-Decoder com *Skip Connections* para recuperação de bordas finas de plumas de gás.
    * Treinamento com **Dice Loss** para lidar com o severo desbalanceamento de classes (o gás ocupa <2% da imagem).

3.  **Inferência Suave:**
    * Reconstrução da imagem via janelas deslizantes com sobreposição (*Gaussian Blending*) para eliminar artefatos de borda.

## 📊 Resultados (Performance)

O modelo foi validado utilizando o dataset *Indian Pines* simulando um cenário de detecção de anomalia crítica (Classe 3).

| Métrica | Valor Final |
| :--- | :--- |
| **IoU (Intersection over Union)** | **0.9881** |
| **Recall (Sensibilidade)** | **1.0000** |
| **Precision** | **0.9881** |
| **F1-Score** | **0.9940** |

### Visualização

O mapa de calor abaixo demonstra a capacidade do modelo de isolar a assinatura espectral do alvo (em vermelho) ignorando o ruído de fundo complexo urbano/rural.

*(Insira aqui a imagem do Overlay que você gerou)*

## 🛠️ Instalação e Uso

### Pré-requisitos
* Python 3.8+
* PyTorch (com suporte a CUDA recomendado)
* Scikit-learn, Spectral, Matplotlib

### Como Rodar
1.  Clone o repositório:
    ```bash
    git clone [https://github.com/SEU_USUARIO/hyperspectral-gas-detection.git](https://github.com/SEU_USUARIO/hyperspectral-gas-detection.git)
    ```
2.  Instale as dependências:
    ```bash
    pip install spectral torch scikit-learn matplotlib
    ```
3.  Execute o notebook `hyperspectral_unet3d.ipynb` no Google Colab ou Jupyter local. O script baixará automaticamente os dados de teste.

## 📜 Citação e Referências

Este trabalho utiliza conceitos de Redes Neurais Convolucionais 3D aplicadas a Sensoriamento Remoto.

* *U-Net: Convolutional Networks for Biomedical Image Segmentation* (Ronneberger et al.)
* *Hyperspectral Image Analysis - Indian Pines Dataset*

---
**Autor:** Igor Emanoel Fernandes Oliveira
*Pesquisador em Visão Computacional e IA*
