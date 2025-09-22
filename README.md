# perceptron

### Documentação do Código do Perceptron

Este documento fornece uma explicação detalhada do código de um Perceptron de camada única, implementado em Python. O Perceptron é um dos algoritmos mais simples de aprendizado de máquina, usado para tarefas de **classificação binária**.

#### **Estrutura Geral do Código**

O programa é dividido em três partes principais:

1.  **A Classe `Perceptron`**: Contém toda a lógica do algoritmo, incluindo o construtor, os métodos de treinamento e teste, e a função de ativação.
2.  **Exemplo de Dados**: Define as amostras de entrada e suas saídas esperadas para o treinamento.
3.  **Execução do Programa**: Cria uma instância da classe `Perceptron`, treina a rede com os dados fornecidos e, em seguida, testa-a com uma nova amostra.

---

### 1. A Classe `Perceptron`

A classe `Perceptron` é a "espinha dorsal" do código. Ela encapsula todos os dados (amostras, pesos, etc.) e as funções (métodos) necessárias para o funcionamento do algoritmo.

#### **`__init__(self, amostras, saidas, taxa_aprendizado=0.1, epocas=1000, limiar=1)`**

* **Propósito**: Este é o **construtor** da classe. Ele é chamado automaticamente quando você cria um novo objeto `Perceptron`. Sua função é inicializar as variáveis que serão usadas por toda a classe.
* **Parâmetros**:
    * `self`: Referência obrigatória para a instância da classe.
    * `amostras`: Uma lista de listas, onde cada lista interna é uma amostra de entrada para o treinamento.
    * `saidas`: Uma lista com os valores de saída esperados (os rótulos) para cada amostra.
    * `taxa_aprendizado`: Define a "velocidade" com que a rede ajusta seus pesos durante o treinamento. Um valor pequeno significa aprendizado lento; um valor grande pode causar instabilidade.
    * `epocas`: O número máximo de vezes que o algoritmo irá passar por todas as amostras de treinamento.
    * `limiar`: Representa o **bias** da rede. É um valor constante adicionado a cada amostra para permitir que a rede aprenda a separar dados que não passam pela origem.

#### **`treinar(self)`**

* **Propósito**: Este método é responsável por **ajustar os pesos** do Perceptron para que ele possa aprender a classificar corretamente as amostras.
* **Como Funciona**:
    1.  **Inicialização de Pesos**: Gera valores aleatórios para os pesos da rede. Existe um peso para cada atributo da amostra, mais um peso adicional para o `limiar` (o bias).
    2.  **Adição do Limiar**: Insere o valor do `limiar` no início de cada amostra. Isso permite que o cálculo `pesos * amostras` inclua o bias automaticamente.
    3.  **Loop de Treinamento**: O treinamento ocorre em um loop `while True`. A cada iteração (uma "época"), o algoritmo percorre todas as amostras.
    4.  **Cálculo da Saída**: Para cada amostra, o **potencial de ativação** é calculado, que é a soma dos produtos de cada peso pelo seu respectivo valor na amostra. Esse valor é então passado pela **função de ativação** (`sinal`) para obter a saída da rede.
    5.  **Ajuste de Pesos**: Se a saída calculada for diferente da saída esperada, o algoritmo calcula o **erro** e ajusta os pesos. O ajuste é proporcional ao erro, à taxa de aprendizado e ao valor da amostra.
    6.  **Condição de Parada**: O loop de treinamento para quando a rede não comete mais erros (ou seja, quando o erro total é `False`) ou quando o número máximo de épocas é atingido.

#### **`teste(self, amostra)`**

* **Propósito**: Este método usa o Perceptron **já treinado** para classificar uma nova amostra, ou seja, prever a sua classe.
* **Como Funciona**:
    1.  Recebe uma amostra de teste.
    2.  Adiciona o `limiar` à amostra de teste (sem modificar a original).
    3.  Calcula o potencial de ativação usando os **pesos ajustados** durante o treinamento.
    4.  Aplica a função de ativação (`sinal`) para obter a classe final.
    5.  Imprime o resultado da classificação.

#### **`sinal(self, u)`**

* **Propósito**: É a **função de ativação** do Perceptron. Sua função é converter o potencial de ativação (`u`) em uma saída binária.
* **Como Funciona**:
    * Se o valor de `u` for maior ou igual a 0, a função retorna `1`.
    * Se o valor de `u` for menor que 0, a função retorna `-1`.

---

### 2. Exemplo de Dados e Execução

As listas `amostras` e `saidas` representam o nosso **conjunto de dados**.

* `amostras`: Contém 30 amostras, cada uma com dois atributos.
* `saidas`: Contém 30 saídas correspondentes, onde `-1` e `1` representam as duas classes que o Perceptron deve aprender a distinguir.

A parte final do código é responsável por:
* `rede = Perceptron(amostras, saidas)`: Cria um objeto chamado `rede`, que é uma instância da classe `Perceptron`.
* `rede.treinar()`: Chama o método de treinamento para a nossa `rede`.
* `rede.teste([0.75, 0.90])`: Chama o método de teste para classificar uma nova amostra `[0.75, 0.90]`.

