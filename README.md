# Algoritmos-de-ordena-o
#include <iostream>
#include <vector>
#include <stdlib.h>

using std::vector;
using std::cout;
using std::endl;


class Quicksort {
 private:

    /**
     * Vetor de inteiros a ser ordenado
     */
    vector<int>& elements;

    /**
     * Tamanho do vetor
     */
    int size;

    /**
     * Método de particionamento que é o núcleo do algoritmo Quicksort.
     * É a implementação utilizando o paradigma dividir para conquistar
     */
    int partition (const int start, const int end)
    {
        int i = start;

        for (int j = start; j < end; j++) {

            /*  Elemento atual menor ou igual ao pivô? */
            if (elements[j] <= elements[end]) {
                swap(i++, j);
            }
        }
        swap(i, end);

        return i;
    }
 /**
     * Método para fazer a troca de dados entre duas posições no vetor
     */
    void swap (const int i, const int j)
    {
        int k = elements[i];
        elements[i] = elements[j];
        elements[j] = k;
    }

    /**
     * Método privado que implementa o Quicksort recursivamente
     */
    void quicksort (const int start, const int end)
    {
        snapshot();

        if (start >= end) return;

        int pivot = partition(start, end);

        quicksort(start, pivot - 1);
        quicksort(pivot + 1, end);
    }

    /**
     * Método utilizado para debugging. Imprime na tela uma 'foto' do vetor
     */
    void snapshot ()
    {
        cout << "[";
        for(auto i = elements.begin(); i < elements.end() - 1; i++) {
            cout << *i << ", ";
        }
        cout << elements.back() << "]" << endl;
    }

 public:
    explicit Quicksort (vector<int>& elements)
    :elements(elements),
     size(elements.size())
    {
    }
  
  


#include <stdio.h>
#include <stdlib.h>

void mergesort(int *v, int n);
void sort(int *v, int *c, int i, int f);
void merge(int *v, int *c, int i, int m, int f);

int main (void) {
  int i;
  int v[8] = { -1, 7, -3, 11, 4, -2, 4, 8 };

  mergesort(v, 8);

  for (i = 0; i < 8; i++) printf("%d ", v[i]);

  putchar('\n');

  return 0;
}

/*
  Dado um vetor de inteiros v e um inteiro n >= 0, ordena o vetor v[0..n-1] em ordem crescente.
*/
void mergesort(int *v, int n) {
  int *c = malloc(sizeof(int) * n);
  sort(v, c, 0, n - 1);
  free(c);
}

/*
  Dado um vetor de inteiros v e dois inteiros i e f, ordena o vetor v[i..f] em ordem crescente.
  O vetor c é utilizado internamente durante a ordenação.
*/
void sort(int *v, int *c, int i, int f) {
  if (i >= f) return;

  int m = (i + f) / 2;

  sort(v, c, i, m);
  sort(v, c, m + 1, f);
  
   /* Se v[m] <= v[m + 1], então v[i..f] já está ordenado. */
  if (v[m] <= v[m + 1]) return;

  merge(v, c, i, m, f);
}


/*
  Dado um vetor v e três inteiros i, m e f, sendo v[i..m] e v[m+1..f] vetores ordenados,
  coloca os elementos destes vetores, em ordem crescente, no vetor em v[i..f].
*/
void merge(int *v, int *c, int i, int m, int f) {
  int z,
      iv = i, ic = m + 1;

  for (z = i; z <= f; z++) c[z] = v[z];

  z = i;

  while (iv <= m && ic <= f) {
    /* Invariante: v[i..z] possui os valores de v[iv..m] e v[ic..f] em ordem crescente. */

    if (c[iv] < c[ic]) v[z++] = c[iv++];
    else /* if (c[iv] > c[ic]) */ v[z++] = c[ic++];
  }

  while (iv <= m) v[z++] = c[iv++];

  while (ic <= f) v[z++] = c[ic++];
}




#include < stdlib.h>
#include < stdio.h>
#include < ctime>

void shellSort(int numbers[], int array_size);


int main(int argc, char const* argv[]){

//seed random number generator
srand((unsigned)time(0)); //Descomente essa linha caso voce queira que o programa gere os numeros aleatorios.

int NUM_ITEMS = 5;
int numbers[5];
int i;

//Descomente o trecho abaixo caso voce queira que o programa gere os numeros aleatorios.
for (i = 0; i < NUM_ITEMS; i++)
numbers[i] = rand();

//numbers[100] = {12,2,6,9,5,7,16,55,32,15}; //Comente esse trecho, caso voce descomente o trecho de codigo acima.

shellSort(numbers, NUM_ITEMS);

printf("Numeros em ordem crescente:\n");
for (i = 0; i < NUM_ITEMS; i++)
printf("%i\n", numbers[i]);

return 0;
}


void shellSort(int numbers[], int array_size)
{
int i, j, increment, temp;

increment = 3;
while (increment > 0)
{
for (i=0; i < array_size; i++)
{
j = i;
temp = numbers[i];
while ((j >= increment) && (numbers[j-increment] > temp))
{
numbers[j] = numbers[j - increment];
j = j - increment;
}
numbers[j] = temp;
}
if (increment/2 != 0)
increment = increment/2;
else if (increment == 1)
increment = 0;
else
increment = 1;
}
}

