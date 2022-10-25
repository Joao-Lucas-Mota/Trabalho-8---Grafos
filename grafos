/* Joao Lucas Mota Nogueira da Costa
Sua  tarefa  será  construir  um  grafo,  com  100  vértices  cujos  valores
serão  aleatoriamente selecinados em um conjunto de inteiros contendo números
inteiros entre 1 e 1000. Cada vértice terá um número aleatório de arestas menor
ou igual a três. Você  deverá  criar  este  grafo,  armazenando  estes  vértices
e  arestas  em  uma  tabela  de adjacências e em uma lista de adjacências,
medindo o tempo necessário para criar estas estruturas de dados. Estas duas
tabelas deverão ser salvas em arquivos de texto chamados de
tabela_adjacencias.txt e lista_adjacencias.txt respectivamente. Estes arquivos
devem ser salvos no site repl.it Para que seja possível verificar as diferenças
de tempos de criação destas estruturas, uma vez que o algoritmo esteja pronto,
você deverá mudar o tamanho do gráfico para 100.000 de itens e repetir o
processo de ciração no mínimo 50 vezes, anotando os tempos de criação
apresentando estas médias para a tabela de adjacencias e para a lista de
adjacencias.
*/

#include <chrono>
#include <fstream>
#include <iostream>
#include <random>
using namespace std;

class TNo { // define uma struct (registro)
public:
  int w;
  TNo *prox;
};

class TGrafo {
private:
  int n;
  int m;
  int **mat_adj;
  TNo **list_adj;

public:
  TGrafo(int n);
  void insereA(int v, int w);
  void show();
  void createFiles();
  ~TGrafo();
};

TGrafo::TGrafo(int n) {
  this->n = n;
  this->m = 0;
  int **mat_adjac = new int *[n];
  for (int i = 0; i < n; i++)
    mat_adjac[i] = new int[n];
  mat_adj = mat_adjac;
  for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
      mat_adj[i][j] = 0;
  TNo **list_adjac = new TNo *[n];
  for (int i = 0; i < n; i++)
    list_adjac[i] = nullptr;
  list_adj = list_adjac;
}

TGrafo::~TGrafo() {
  for (int i = 0; i < n; i++) {
    TNo *no = list_adj[i];
    TNo *ant = nullptr;
    while (no) {
      ant = no;
      no = no->prox;
      delete ant;
    }
  }
  delete[] list_adj;
  n = 0;
  m = 0;
  delete[] * mat_adj;
  cout << "Espaco liberado";
}

void TGrafo::insereA(int v, int w) {
  if (mat_adj[v][w] == 0) {
    mat_adj[v][w] = 1;
    m++;
  }
  TNo *novoNo;
  TNo *no = list_adj[v];
  TNo *ant = nullptr;
  while (no && w >= no->w) {
    if (w == no->w)
      return;
    ant = no;
    no = no->prox;
  };
  novoNo = new TNo;
  novoNo->w = w;
  novoNo->prox = no;
  if (ant == nullptr) {
    list_adj[v] = novoNo;
  } else
    ant->prox = novoNo;
}

void TGrafo::show() {
  cout << "Numero de vertices: " << n << endl;
  cout << "Numero de arestas: " << m << endl;
  cout << "\nMatriz de Adjacencia:";
  for (int i = 0; i < n; i++) {
    cout << "\n";
    for (int w = 0; w < n; w++)
      if (mat_adj[i][w] == 1)
        cout << "Adj[" << i << "," << w << "]= 1"
             << " ";
      else
        cout << "Adj[" << i << "," << w << "]= 0"
             << " ";
  }
  cout << "\n\nFim da impressao da matriz do grafo." << endl;

  cout << "\nLista de Adjacencia:";
  for (int i = 0; i < n; i++) {
    cout << "\n" << i << ": ";
    // Percorre a lista na posição i do vetor
    TNo *no = list_adj[i];
    while (no) {
      cout << no->w << " ";
      no = no->prox;
    }
  }
  cout << endl << "\nFim da impressao da lista do grafo.\n" << endl;
}

void TGrafo::createFiles() {
  ofstream file1, file2;
  file1.open("Matriz de Adjacencia.txt");

  file1 << "Numero de vertices: " << n << endl;
  file1 << "Numero de arestas: " << m << endl;
  file1 << "\nMatriz de Adjacencia:";
  for (int i = 0; i < n; i++) {
    file1 << "\n";
    for (int w = 0; w < n; w++)
      if (mat_adj[i][w] == 1)
        file1 << "Adj[" << i << "," << w << "]= 1"
              << " ";
      else
        file1 << "Adj[" << i << "," << w << "]= 0"
              << " ";
  }
  file1.close();

  file2.open("Lista de Adjacencia.txt");
  file2 << "Numero de vertices: " << n << endl;
  file2 << "Numero de arestas: " << m << endl;
  file2 << "\nLista de Adjacencia:";
  for (int i = 0; i < n; i++) {
    file2 << "\n" << i << ": ";
    TNo *no = list_adj[i];
    while (no) {
      file2 << no->w << " ";
      no = no->prox;
    }
  }
  file2.close();
}

int main() {
  TGrafo g(10);
  random_device a;
  mt19937 gerador(a());
  uniform_int_distribution<int> range(1, 10);
  auto start = chrono::steady_clock::now();
  for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 3; j++) {
      int x = range(gerador);
      if (i != x)
        g.insereA(i, x);
    }
  }
  auto end = chrono::steady_clock::now();
  double tempo =
      chrono::duration_cast<chrono::nanoseconds>(end - start).count();
  g.show();
  cout << "Tempo utilizado para criar a matriz e a lista de adjacencias: "
       << tempo << " Nanossegundos" << endl;
  g.createFiles();
}
