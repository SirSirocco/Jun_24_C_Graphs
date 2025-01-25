# Jun_24_C_Graphs

[🇧🇷 Leia em Português](#português) | [🇺🇸 Read in English](#english)

## Português

**Data:** Junho, 2024.

**Integrantes:**

- Mayara Ramos Damazio
- Pedro de Almeida Barizon

**Objetivo:** Implementar dois dos principais algoritmos relacionados a grafos: o algoritmo de Kruskal e o de Dijkstra.

## Estrutura dos Programas

### Programa de Kruskal

O programa é composto de cinco módulos:

- `kruskal_main.c`, responsável pela execução do programa que realiza o algoritmo de Kruskal;
- `grafos.c`, responsável pela manipulação de grafos;
- `grafos.h`, responsável pelas declarações das funções do grafos.c e das estruturas node, grafo e aresta;
- `kruskal.c`, responsável pelo algoritmo de Kruskal;
- `kruskal.h`, responsável pelas declarações das funções do kruskal.c e da estrutura noConj.

### Programa de Dijkstra

O programa é composto de cinco módulos:

- `dijkstra_main.c`, responsável pela execução do programa que realiza o algoritmo de Dijkstra;
- `grafos.c`, responsável pela manipulação de grafos;
- `grafos.h`, responsável pelas declarações das funções do grafos.c e das estruturas node, grafo e aresta;
- `dijkstra.c`, responsável pelo algoritmo de Dijkstra;
- `dijkstra.h`, responsável pelas declarações das funções do dijkstra.c.

## Estruturas Utilizadas

### `grafos.c`

```c
struct node {
    int i;
    Peso peso;
    struct node* prox;
};

struct grafo {
    struct node** vViz;
    int nVert;
    int nArest;
};

struct aresta {
    int i;
    int j;
    Peso peso;
};
typedef struct node No;
typedef struct grafo Grafo;
typedef struct aresta Aresta;
```

### `kruskal.c`

```c
struct noConj {
    int chave;
    struct noConj* rep;
};
typedef struct noConj NoConj;
```

## Funções Utilizadas

### `grafos.c`

```c
Grafo* criaGrafo(int nVert);
void printaMonografo(Grafo* grafo);
void printaDigrafo(Grafo* grafo);
void printaArestas(Aresta* vArestas, int nArest);
void ordenaArestas(Aresta* vArestas, int nArest);
void adicionaArestaMonografo(Grafo* grafo, Aresta* arestas, int nArest);
void adicionaArestaDigrafo(Grafo* grafo, Aresta* arestas, int nArest);
void liberaGrafo(Grafo* grafo);
```

### `kruskal.c`

```c
void iniciaVertices(NoConj* vVertices, int nVert);
void printaVertices(NoConj* vVertices, int nVert);
void fusion(int num1, int num2, NoConj* vVertices, int nVert);
NoConj* find(int num1, NoConj* vVertices);
Grafo* criaArvMinima(Aresta* vArestas, int nArest, NoConj* vVertices, int nVert);
```

### `dijkstra.c`

```c
void dijkstra(Grafo* grafo, int iOrigem);
```

## Solução

### Kruskal

Ao início, são declarados o vetor de arestas, um vetor de estruturas do tipo `NoConj`, que representa os _singletons_, duas variáveis do tipo ponteiro para `Grafo` e duas do tipo `int`, que contêm as informações dos grafos. Uma das variáveis do tipo `Grafo` recebe o endereço do grafo gerado pela criaGrafo, e depois a função printaMonografo o exibe. Após a exibição do grafo inteiro, é iniciado o algoritmo de Kruskal. Inicialmente, o vetor de _singletons_ é iniciado e o de arestas é ordenado. Depois, é chamada a função `criaArvMinima`. Nela, um grafo é iniciado, ou seja, é alocado apenas o vetor de ponteiros que irão apontar para as listas encadeadas de cada vértice. Ao percorrer o vetor de arestas, para cada uma delas, ele realiza um _find_ dos vértices que formam essa aresta e, para isso, ele chama a função `find`. Essa função funciona recursivamente e procura o endereço do representante do elemento. Se os dois representantes de ambos os vértices forem diferentes, é chamada a função `adicionaArestaMonografa` que vai adicionar um novo elemento na lista encadeada da posição do vértice. Depois é chamada a função `fusion` que, levando em conta a altura, coloca os dois vértices no mesmo conjunto. Após o final da iteração das arestas, o grafo que representa a árvore é retornado para a outra variável do tipo ponteiro para `Grafo` e, novamente, é chamada a `printaMonografo`, que exibe a árvore mínima retornada. Por fim, as memórias de ambos os grafos são liberadas com a função `liberaGrafo`.

### Dijkstra

Ao início, é construído o grafo com base em um conjunto de arestas previamente definido. Exibe-se o grafo antes e depois das inserções. Em seguida, aplica-se a dijkstra ao grafo, passando-se o índice zero como origem. A função imprime uma tabela com as condições iniciais (Visita 0) e, a cada nova visita a um vértice pelo algoritmo, exibe a tabela de Dijkstra atualizada. Evidentemente, a última tabela printada é aquela com as distâncias mínimas à origem.

## Observações e Conclusões

Os algoritmos de Kruskal e de Dijkstra revelaram-se surpreendentemente fáceis de serem implementados — ainda mais com o prévio desenvolvimento do módulo `grafos.c` —, com pleno funcionamento e êxito em todos os testes. Quanto a dificuldades de implementação, estas, sendo pequenas, foram prontamente resolvidas com o auxílio do depurador. Por fim, os programas foram compilados sem erro usando-se o ambiente de desenvolvimento do replit, que se mostrou conveniente por permitir edição simultânea do código pelos dois integrantes do grupo.

## English

**Data:** June, 2024.

**Authors:**

- Mayara Ramos Damazio
- Pedro de Almeida Barizon

**Objective:** Implement two of the main graph-related algorithms: Kruskal's algorithm and Dijkstra's algorithm.

## Program Structure

### Kruskal Program

The program consists of five modules:

- `kruskal_main.c`, responsible for executing the program that implements Kruskal's algorithm;
- `grafos.c`, responsible for graph manipulation;
- `grafos.h`, responsible for declaring the functions from `grafos.c` and the structures `node`, `grafo` (graph), and `aresta` (edge);
- `kruskal.c`, responsible for Kruskal's algorithm;
- `kruskal.h`, responsible for declaring the functions from `kruskal.c` and the `noConj` structure.

### Dijkstra Program

The program consists of five modules:

- `dijkstra_main.c`, responsible for executing the program that implements Dijkstra's algorithm;
- `grafos.c`, responsible for graph manipulation;
- `grafos.h`, responsible for declaring the functions from `grafos.c` and the structures `node`, `grafo` (graph), and `aresta` (edge);
- `dijkstra.c`, responsible for Dijkstra's algorithm;
- `dijkstra.h`, responsible for declaring the functions from `dijkstra.c`.

## Data Structures Used

### `grafos.c`

```c
struct node {
    int i;
    Peso peso;
    struct node* prox;
};

struct grafo {
    struct node** vViz;
    int nVert;
    int nArest;
};

struct aresta {
    int i;
    int j;
    Peso peso;
};
typedef struct node No;
typedef struct grafo Grafo;
typedef struct aresta Aresta;
```

### `kruskal.c`

```c
struct noConj {
    int chave;
    struct noConj* rep;
};
typedef struct noConj NoConj;
```

## Functions Used

### `grafos.c`

```c
Grafo* criaGrafo(int nVert);
void printaMonografo(Grafo* grafo);
void printaDigrafo(Grafo* grafo);
void printaArestas(Aresta* vArestas, int nArest);
void ordenaArestas(Aresta* vArestas, int nArest);
void adicionaArestaMonografo(Grafo* grafo, Aresta* arestas, int nArest);
void adicionaArestaDigrafo(Grafo* grafo, Aresta* arestas, int nArest);
void liberaGrafo(Grafo* grafo);
```

### `kruskal.c`

```c
void iniciaVertices(NoConj* vVertices, int nVert);
void printaVertices(NoConj* vVertices, int nVert);
void fusion(int num1, int num2, NoConj* vVertices, int nVert);
NoConj* find(int num1, NoConj* vVertices);
Grafo* criaArvMinima(Aresta* vArestas, int nArest, NoConj* vVertices, int nVert);
```

### `dijkstra.c`

```c
void dijkstra(Grafo* grafo, int iOrigem);
```

## Solution

### Kruskal

Initially, the program declares an array of edges, an array of structures of type `NoConj` representing the singletons, two pointer variables to `Grafo`, and two integer variables containing graph information. One of the `Grafo` variables receives the address of the graph generated by `criaGrafo`, and the function `printaMonografo` displays it. After displaying the entire graph, the Kruskal algorithm starts. Initially, the singleton array is initialized, and the edges array is sorted. Then, the `criaArvMinima` function is called. In this function, a graph is initialized by allocating only the array of pointers pointing to the linked lists of each vertex. As the edges array is traversed, for each edge, a `find` is performed on the vertices forming that edge by calling the `find` function. This function operates recursively, looking for the representative of the element. If the representatives of both vertices are different, the `adicionaArestaMonografo` function is called to add a new element to the linked list of the vertex's position. Then, the `fusion` function is called, which considers the height and places the two vertices in the same set. After iterating through all the edges, the graph representing the tree is returned to the second pointer variable to `Grafo`, and `printaMonografo` is called again to display the returned minimum spanning tree. Finally, the memory of both graphs is released using the `liberaGrafo` function.

### Dijkstra

Initially, the graph is constructed based on a predefined set of edges. The graph is displayed before and after the insertions. Then, Dijkstra's algorithm is applied to the graph, with index zero as the source. The function prints a table with the initial conditions (Visit 0), and for each new vertex visit by the algorithm, it updates the Dijkstra table. Naturally, the last printed table contains the minimum distances to the source.

## Observations and Conclusions

Kruskal's and Dijkstra's algorithms were surprisingly easy to implement, especially with the prior development of the `grafos.c` module. Both algorithms functioned correctly and successfully passed all tests. Implementation difficulties were minimal and promptly resolved with the help of a debugger. Finally, the programs were compiled without errors using the Replit development environment, which proved convenient for simultaneous code editing by both group members.
