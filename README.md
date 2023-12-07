# Projeto de Automatização de Reconhecimento de Notas Fiscais para Gastos Público

Este projeto tem como objetivo automatizar o processo de reconhecimento de texto em notas fiscais, utilizando técnicas de OCR (Optical Character Recognition) e Aprendizado de Máquina. O código está implementado em um notebook Jupyter e utiliza as seguintes bibliotecas:

- PyMuPDF
- pytesseract
- opencv-python-headless
- pillow
- pandas

## Passos para Executar o Notebook

### 1. Instalar as Dependências

Certifique-se de ter todas as bibliotecas necessárias instaladas. Execute o seguinte comando para instalá-las:

```
!pip install PyMuPDF
!pip install pytesseract
!pip install opencv-python-headless
!pip install pillow
!pip install pandas

```
### 2. Configurar o Tesseract OCR

Certifique-se de que o Tesseract OCR esteja instalado no seu sistema. No código, é configurado o caminho para o executável do Tesseract OCR. Adapte essa configuração conforme necessário para o seu ambiente.

```
pytesseract.pytesseract.tesseract_cmd = "C:/Tesseract-OCR/tesseract.exe"
```

### 3. Preparação dos dados
Lembre-se que as notas fiscais deve estar no formato de 90 graus para o Pytesseract conseguir ler elas corretamente. Foi realizado um trabalho manual para girar as notas na orientação correta.

### 4. Baixar o Modelo de Treinamento para OCR
Se você precisar de suporte para o idioma português, baixe o modelo de treinamento específico para o português usando o comando abaixo:

```
# Baixar o modelo de treinamento para o idioma português
!wget https://github.com/tesseract-ocr/tessdata/raw/main/por.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

### 5. Executar o Notebook
Abra o notebook Jupyter e execute cada célula sequencialmente. Certifique-se de ajustar o caminho do arquivo PDF de entrada, se necessário.
