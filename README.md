#include <stdio.h>
#include <stdlib.h>

typedef struct No {
    int valor;
    struct No *prox;
} No;

void inserir_inicio(No **lista, int valor) {
    No *novo = (No*) malloc(sizeof(No));
    if (!novo) {
        printf("Erro ao alocar memoria\n");
        return;
    }
    novo->valor = valor;
    novo->prox = *lista;
    *lista = novo;
}

void inserir_fim(No **lista, int valor) {
    No *novo = (No*) malloc(sizeof(No));
    if (!novo) {
        printf("Erro ao alocar memoria\n");
        return;
    }
    novo->valor = valor;
    novo->prox = NULL;

    if (*lista == NULL) {

        *lista = novo;
    } else {
        No *aux = *lista;
      
        while (aux->prox != NULL) {
            aux = aux->prox;
        }
        aux->prox = novo;
    }
}

void imprimir_lista(No *lista) {
    No *aux = lista;
    while (aux != NULL) {
        printf("%d -> ", aux->valor);
        aux = aux->prox;
    }
    printf("NULL\n");
}

void liberar_lista(No **lista) {
    No *aux;
    while (*lista != NULL) {
        aux = *lista;
        *lista = (*lista)->prox;
        free(aux);
    }
}

int main() {
    No *lista = NULL;

    inserir_fim(&lista, 10);
    inserir_inicio(&lista, 5);
    inserir_fim(&lista, 20);
    inserir_inicio(&lista, 1);

    imprimir_lista(lista);

    liberar_lista(&lista);

    return 0;
}
