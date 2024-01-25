
# Machine Learning na Prática no Azure ML

Neste laboratório, utilizarei o recurso de aprendizado de máquina automatizado no Azure Machine Learning para treinar e avaliar um modelo de aprendizado de máquina. 


## Requisitos conta Azure

Acesse ao portal de [Azure](https://portal.azure.com) com suas credenciais. 
Selecione + Criar um recurso, e pesquise Azure Machine Learning  com as seguintes configurações:


  - Configurações básicas:
```bash
    Nome do trabalho: mslearn-bike-automl
    Nome do novo experimento: mslearn-bike-rental
    Descrição: Aprendizado automático de máquina para previsão de aluguel de bicicletas
    Tags: nenhum
```
  - Tipo de tarefa e dados:
```bash
    Selecione o tipo de tarefa: Regressão
    Selecione o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações:
        Tipo de dados:
            Nome: bike-rentals
            Descrição: Dados históricos de aluguel de bicicletas
            Tipo: Tabular
        Fonte de dados:
Selecionar de arquivos da Web
        URL da Web:
            URL da Web: https://aka.ms/bike-rentals
            Ignorar validação de dados: não selecionar
        Configurações:
            File format (Formato de arquivo): Delimitado
            Delimitador: Comma
            Codificação: UTF-8
            Cabeçalhos de coluna: Somente o primeiro arquivo tem cabeçalhos
            Pular linhas: Nenhum
            O conjunto de dados contém dados com várias linhas: não selecionar
        Esquema:
            Include all columns other than Path (Incluir todas as colunas que não sejam Path)
            Revise os tipos detectados automaticamente
```
Selecione Create (Criar). Depois que o conjunto de dados for criado, selecione o conjunto de dados bike-rentals para continuar a enviar o trabalho de ML automatizado.

- Configurações da tarefa:

    Tipo de tarefa: Regressão
    Conjunto de dados: bike-rentals
    Coluna de destino: Aluguel (número inteiro)
    Definições de configuração adicionais:
        Métrica primária: Normalized root mean squared error (erro quadrático médio normalizado)
        Explicar o melhor modelo: Não selecionado
        Usar todos os modelos suportados: Não selecionado. Você restringirá o trabalho para tentar apenas alguns algoritmos específicos.
        Modelos permitidos: Selecione apenas RandomForest e LightGBM - normalmente você gostaria de testar o maior número possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.
    Limites: Expanda esta seção
        Máximo de tentativas: 3
        Máximo de tentativas simultâneas: 3
        Máximo de nós: 3
        Limite de pontuação métrica: 0,085 (de modo que, se um modelo atingir uma pontuação métrica de erro quadrático médio normalizado de 0,085 ou menos, o trabalho será encerrado).
        Tempo limite: 15
        Tempo limite de iteração: 15
        Ativar o encerramento antecipado: Selecionado
    Validação e teste:
        Tipo de validação: Divisão de treinamento-validação
        Porcentagem de dados de validação: 10
        Conjunto de dados de teste: Nenhum

- Servidor

        Selecione o tipo de computação: Sem servidor
        Tipo de máquina virtual: CPU
        Nível da máquina virtual: Dedicada
        Tamanho da máquina virtual: Standard_DS3_V2*
        Número de instâncias: 1

Implantar e testar o modelo
  Name: predict-rentals
  Description: Predict cycle rentals
  Compute type: Azure Container Instance
  Enable authentication: Selected

- Teste do serviço implantado
    [input](https://github.com/juanfisicobr/AzureMachineL/input.json)
Resposta do modelo
```bash
{
  "Results":[
    0:float 399.8883147614036
  ]
}
```
    
