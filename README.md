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

Você pode ver um exemplo de nota [Clicando aqui](https://github.com/nicolemartins7/nibi/blob/main/exemplo_nota_rotacionada.pdf).



### 4. Baixar o Modelo de Treinamento para OCR
Se você precisar de suporte para o idioma português, baixe o modelo de treinamento específico para o português usando o comando abaixo:

```
# Baixar o modelo de treinamento para o idioma português
!wget https://github.com/tesseract-ocr/tessdata/raw/main/por.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

### 4.1 Busca por Palavras-Chave

- contains_keywords(text, keywords):

Esta função verifica se uma string contém qualquer uma das palavras-chave fornecidas.
Retorna a contagem de palavras-chave encontradas e a lista das palavras encontradas.

- search_text_from_df(df, n_rows_to_search, positive_keywords, negative_keywords):

Esta função percorre as linhas de um DataFrame, buscando palavras-chave positivas e negativas em cada página.
Retorna um DataFrame com informações sobre a busca, incluindo o número da página, o número de palavras-chave encontradas, as palavras-chave encontradas (tanto positivas quanto negativas), o texto encontrado na página, entre outras informações.

- extract_numerical_values(text):

Extrai valores numéricos (incluindo decimais) de uma string usando expressões regulares.

- extract_money_values(text):

Extrai valores monetários formatados de uma string usando expressões regulares.

- extract_dates(text):

Extrai datas no formato "dd/mm/yyyy" de uma string usando expressões regulares.

- find_date(text):

Busca a primeira ocorrência de uma data no formato "dd/mm/yyyy" em uma string.

- find_cnpj(text):

Busca a primeira ocorrência de um CNPJ em uma string.

- find_mode(extract_money_values):

Calcula a moda (valor mais frequente) de uma lista de valores monetários.

### 4.2 Tokenização BERT e Vetorização TF-IDF

O código inclui uma função chamada bert_tokenizer, que tem como objetivo realizar a tokenização usando o modelo BERT e, em seguida, vetorizar os textos usando o método TF-IDF (Term Frequency-Inverse Document Frequency). Aqui está uma explicação da função:

- Importação de Bibliotecas:

Importa as bibliotecas necessárias, incluindo BertTokenizer da biblioteca transformers e TfidfVectorizer da biblioteca scikit-learn.

- Carregamento do Tokenizer BERT:

Carrega o tokenizer BERT pré-treinado do modelo 'bert-base-uncased'. Este modelo BERT é treinado em texto em inglês e converte o texto em uma representação numérica usando tokens.

- Tokenização usando TF-IDF:

Utiliza a técnica de vetorização TF-IDF para converter os textos em uma matriz TF-IDF.
Cada linha da matriz representa um texto, e cada coluna representa uma palavra (ou token) presente nos textos. Os valores na matriz são calculados com base na frequência dos tokens nos textos, ponderados pela frequência inversa nos documentos (TF-IDF).

- Retorno da Matriz TF-IDF:

Retorna a matriz TF-IDF resultante.

### 4.3 Treinamento do modelo

Esta seção do código é dedicada ao treinamento de vários modelos de aprendizado de máquina para tarefas de classificação utilizando dados textuais. Os modelos considerados para treinamento incluem Máquina de Vetores de Suporte (SVM), Random Forest, XGBoost, Regressão Logística e Gradient Boosting. O processo de treinamento e avaliação envolve a tokenização dos dados textuais usando os métodos de vetorização BERT e TF-IDF. O desempenho de cada modelo é avaliado em conjuntos de dados de treinamento e teste, e uma análise abrangente é fornecida por meio de várias métricas e relatórios de classificação.

#### Pré-processamento de Dados:

Os dados textuais são tokenizados usando o tokenizer BERT e convertidos em vetores TF-IDF usando o TfidfVectorizer.

#### Seleção do Modelo:

Vários modelos de classificação são considerados, incluindo SVM, Random Forest, XGBoost, Regressão Logística e Gradient Boosting.

#### Treinamento e Avaliação:

Cada modelo é treinado usando o conjunto de dados de treinamento, e seu desempenho é avaliado nos conjuntos de dados de treinamento e teste.

#### Cálculo de Métricas:

Métricas como acurácia, precisão, recall e F1-score são calculadas para cada modelo nos conjuntos de dados de treinamento e teste.

#### Relatórios de Classificação:

Relatórios de classificação detalhados, incluindo precisão, recall e F1-score para cada classe, são gerados para o conjunto de dados de teste.
#### Resultados e Análises:

Os resultados são apresentados em forma tabular, mostrando as métricas de desempenho de cada modelo nos conjuntos de dados de treinamento e teste.

#### Saídas Adicionais:

Para cada modelo, é criado um DataFrame contendo informações sobre as previsões, pontuações de confiança e outros detalhes relevantes para análises adicionais.

### 5. Executar o Notebook
Abra o notebook Jupyter e execute cada célula sequencialmente. Certifique-se de ajustar o caminho do arquivo PDF de entrada, se necessário.

### 6. Considerações finais

Você pode encontrar os resultados do csv nos documentos ocr-teste.csv, ocr-treino.csv e resultados.csv

### Autores

- Gabriel Gutierrez Pereira
- Hugo Amorim Martins
- Nicole Martins dos Santos

