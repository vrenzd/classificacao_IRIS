# Exercício Prático: Classificação Botânica com Árvores de Decisão


## 1. Requisitos

As bibliotecas necessárias para a execução do código (listadas também no arquivo `requirements.txt`):

Para instalar todas de uma vez, abra o terminal ou prompt de comando na pasta do projeto e execute:

```bash
pip install -r requirements.txt
```

## 2. Como usar o Notebook

1. Certifique-se de que os requisitos foram instalados conforme a instrução acima.
2. Abra o arquivo `classificacao_iris_arvore_decisao.ipynb` utilizando uma IDE ou aplicativo de sua preferência (como Jupyter Notebook, JupyterLab, ou VS Code).
3. Execute as células de código de forma sequencial, de cima para baixo (na maioria das IDEs usa-se `Shift + Enter`).
4. Ao longo da execução, você acompanhará a carga do dataset das plantas, manipulação dos dados, treinamento do modelo (com e sem restrição de profundidade), e por fim, a geração visual do diagrama da Árvore de Decisão treinado.

## 3. Guia de Análise (O que observar)

**Qual característica (feature) a árvore escolheu para o primeiro corte (topo)?**
A árvore escolheu a característica **`petal_width`** (largura da pétala) para o primeiro corte no nó raiz. *(Nota: Dependendo do random_state ou de pequenas alterações nos dados, a árvore pode alternar com `petal_length`, mas em ambos os casos representam as features mais discriminativas deste agrupamento).*

**Por que ela é considerada a mais importante?**
No algoritmo CART (Classification and Regression Trees), a funcionalidade escolhida para o primeiro corte é a que resulta no **maior Ganho de Informação** ou, equivalentemente, na **maior redução da impureza (Índice Gini)**. Essa característica foi a que conseguiu dividir de forma mais eficiente as diferentes espécies logo de início – separando totalmente os registros da espécie *Iris-setosa* no ramo esquerdo.

**Compare o Índice Gini da raiz com o das folhas. O que aconteceu com a "impureza" dos dados conforme descemos na árvore?**
Na raiz da árvore, o Índice Gini é alto (aproximadamente `0.666`), indicando uma maior "impureza" (uma vez que os dados estão perfeitamente distribuídos entre as três espécies com 50 amostras cada). 
Conforme descemos na árvore, a impureza **diminui progressivamente**. O Índice Gini fica progressivamente menor à medida que percorremos até os nós folha. Em uma árvore perfeitamente treinada (sem limite de profundidade), todas as folhas terão um Índice Gini igual a `0.0`, indicando pureza total (apenas uma classe por folha). Na nossa árvore construída com `max_depth=3`, observamos valores bem próximos ou iguais a zero em suas bordas e folhas.

**No gráfico da árvore, identifique se existe algum nó que conseguiu separar 100% de uma espécie Gini = 0.0.**
**Sim!** Logo abaixo do nó raiz da árvore, o corte realizado separou perfeitamente todos os 50 exemplares amostrados de **Iris-setosa** que foram desviados para o nó da esquerda. Esse nó é uma folha com **Índice Gini = 0.0**, ou seja, possui 100% de pureza contendo exclusidade de amostras de apenas uma espécie.
