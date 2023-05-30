# pratica-prof
# Marco Antônio Sena Barbosa
Repo Prática Profissional
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CONTATOS 100

struct Operadora {
    char nome[20];
};

struct TipoCelular {
    char nome[20];
};

struct Contato {
    char nome[50];
    char telefone[20];
    char email[50];
    struct Operadora operadora;
    struct TipoCelular tipoCelular;
};

struct Agenda {
    struct Contato contatos[MAX_CONTATOS];
    int numContatos;
};

void adicionarContato(struct Agenda *agenda) {
    if (agenda->numContatos >= MAX_CONTATOS) {
        printf("A agenda está cheia.\n");
        return;
    }

    struct Contato novoContato;

    printf("Nome: ");
    scanf("%s", novoContato.nome);
    printf("Telefone: ");
    scanf("%s", novoContato.telefone);
    printf("Email: ");
    scanf("%s", novoContato.email);
    printf("Operadora: ");
    scanf("%s", novoContato.operadora.nome);
    printf("Tipo de celular: ");
    scanf("%s", novoContato.tipoCelular.nome);

    agenda->contatos[agenda->numContatos] = novoContato;
    agenda->numContatos++;

    printf("Contato adicionado com sucesso.\n");
}

void visualizarContatos(struct Agenda agenda) {
    if (agenda.numContatos == 0) {
        printf("Agenda vazia.\n");
        return;
    }

    printf("Contatos:\n");

    for (int i = 0; i < agenda.numContatos; i++) {
        printf("Nome: %s\n", agenda.contatos[i].nome);
        printf("Telefone: %s\n", agenda.contatos[i].telefone);
        printf("Email: %s\n", agenda.contatos[i].email);
        printf("Operadora: %s\n", agenda.contatos[i].operadora.nome);
        printf("Tipo de celular: %s\n", agenda.contatos[i].tipoCelular.nome);
        printf("--------------------------\n");
    }
}

void editarContato(struct Agenda *agenda) {
    if (agenda->numContatos == 0) {
        printf("Agenda vazia.\n");
        return;
    }

    char nomeBusca[50];
    printf("Digite o nome do contato que deseja editar: ");
    scanf("%s", nomeBusca);

    for (int i = 0; i < agenda->numContatos; i++) {
        if (strcmp(agenda->contatos[i].nome, nomeBusca) == 0) {
            printf("Digite os novos dados para o contato:\n");
            printf("Nome: ");
            scanf("%s", agenda->contatos[i].nome);
            printf("Telefone: ");
            scanf("%s", agenda->contatos[i].telefone);
            printf("Email: ");
            scanf("%s", agenda->contatos[i].email);
            printf("Operadora: ");
            scanf("%s", agenda->contatos[i].operadora.nome);
            printf("Tipo de celular: ");
            scanf("%s", agenda->contatos[i].tipoCelular.nome);

            printf("Contato editado com sucesso.\n");
            return;
        }
    }

    printf("Contato não encontrado.\n");
}

void removerContato(struct Agenda *agenda) {
    if (agenda->numContatos == 0) {
        printf("Agenda vazia.\n");
        return;
    }

    char nomeBusca[50];
    printf("Digite o nome do contato que deseja remover: ");
    scanf("%s", nomeBusca);

    for (int i = 0; i < agenda->numContatos; i++) {
        if (strcmp(agenda->contatos[i].nome, nomeBusca) == 0) {
            for (int j = i; j < agenda->numContatos - 1; j++) {
                agenda->contatos[j] = agenda->contatos[j + 1];
            }

            agenda->numContatos--;

            printf("Contato removido com sucesso.\n");
            return;
        }
    }

    printf("Contato não encontrado.\n");
}

int main() {
    struct Agenda minhaAgenda;
    minhaAgenda.numContatos = 0;
    int opcao;

    do {
        printf("\nMenu:\n");
        printf("1 - Adicionar Contato\n");
        printf("2 - Visualizar Contatos\n");
        printf("3 - Editar Contato\n");
        printf("4 - Remover Contato\n");
        printf("0 - Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                adicionarContato(&minhaAgenda);
                break;
            case 2:
                visualizarContatos(minhaAgenda);
                break;
            case 3:
                editarContato(&minhaAgenda);
                break;
            case 4:
                removerContato(&minhaAgenda);
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida.\n");
                break;
        }
    } while (opcao != 0);

    return 0;
}

