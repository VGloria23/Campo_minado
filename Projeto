#include<stdio.h>
#include<stdlib.h>
#include <time.h>
#include<string.h>
#define A 65
#define A_LOWER 97
#define BLUE "\x1b[96m"
#define YELLOW "\x1b[93m"
#define RED "\x1b[91m"
#define PURPLE "\x1b[95m"
#define GREEN "\x1b[92m"
#define RESET "\x1b[0m"

struct cell{
  int val;
  int dis;
}; typedef struct cell cell;
  /*cell val = 0 -> normal*/
  /*cell val = 9 -> bomba*/
  /*cell dis = 0 -> hidden cell*/
  /*cell dis = 1 -> display cell*/
  /*cell dis = 2 -> flag*/
  /*cell dis = 3 -> bomb*/

int randN(int min, int max){
  /*Gera um inteiro entre o mínimo e o máximo*/
  return rand() % (max + 1 - min) + min;
}

int adj_bombs(cell** mat, int a, int b, int n){
  /*recebe uma posição no mapa e retorna quantas bombas estão adjacentes aquela posição*/
  int adj=0;
  
  /*leste*/
  if(b+1<n){
    if(mat[a][b+1].val == 9){
      adj++;
    }
  }
  /*oeste*/
  if(b-1>=0){
    if(mat[a][b-1].val == 9){
      adj++;
    }
  }
  /*sul*/
  if(a+1<n){
    if(mat[a+1][b].val == 9){
      adj++;
    }
  }
  /*sudeste*/
  if(a+1<n && b+1<n){
    if(mat[a+1][b+1].val == 9){
      adj++;
    }
  }
  /*sudoeste*/
  if(a+1<n && b-1>=0){
    if(mat[a+1][b-1].val == 9){
      adj++;
    }
  }
  /*norte*/
  if(a-1>=0){
    if(mat[a-1][b].val == 9){
      adj++;
    }
  }
  /*nordeste*/
  if(a-1>=0 && b+1<n){
    if(mat[a-1][b+1].val == 9){
      adj++;
    }
  }
  /*noroeste*/
  if(a-1>=0 && b-1>=0){
    if(mat[a-1][b-1].val == 9){
      adj++;
    }
  }
  return adj;
}

cell** criar_jogo(int n){
  /*cell val = 0 -> normal*/
  /*cell val = 9 -> bomba*/
  
  /*aloca a memória para o tabuleiro*/
  cell** mat = malloc(n*sizeof(cell*));
  for(int i=0; i<n; i++){
    cell* test = malloc(n*sizeof(cell));
    mat[i] = test;
  }

  /*coloca 0 em todos os valores*/
  for(int i=0; i<n; i++){
    for(int j=0; j<n; j++){
      mat[i][j].val = 0;
      mat[i][j].dis = 0;
    }
  }

  /*alocar bombas, 9 = bomba*/
  int a, b, bombs = n*n/8;

  while(bombs!=0){
    a=randN(0,n-1);
    b=randN(0,n-1);
    if(mat[a][b].val != 9){
      mat[a][b].val = 9;
      bombs--;
    }
  }

  /*mostrar valores adjacentes*/
  for(int i=0; i<n; i++){
    for(int j=0; j<n; j++){
      if(mat[i][j].val != 9){
        mat[i][j].val = adj_bombs(mat, i, j, n);
      }
    }
  }

  return mat;
}

void mostrar_tabuleiro(cell** mat, int n, int cond){
  /*cell dis = 0 -> hidden cell*/
  /*cell dis = 1 -> display cell*/
  /*cell dis = 2 -> flag*/
  /*cell dis = 3 -> bomb*/
  /*cond = 1 -> jogador perdeu*/

  printf("  ");
  for(int i=A; i<A+n; i++){
    printf("%c ", i);
  }
  printf("\n");

  /*se o jogador perdeu, mostre todas as bombas*/
  if(cond == 1){
    for(int i=0; i<n; i++){
      for(int j=0; j<n; j++){
        if(mat[i][j].val == 9){
          mat[i][j].dis = 3;
        } else {
          mat[i][j].dis = 1;
        }
      }
    }
  }

  /*mostre o tabuleiro*/
  for(int i=0; i<n; i++){
    printf("%c ", A+i);
    for(int j=0; j<n; j++){
      if(mat[i][j].dis == 0){
        printf("🟩 ");
      } else if(mat[i][j].dis == 1){
        if(mat[i][j].val == 0){
          printf("⬜ ");
        } else if(mat[i][j].val == 1){
          printf(BLUE "1 " RESET);
        } else if(mat[i][j].val == 2){
          printf(YELLOW "2 " RESET);
        } else if(mat[i][j].val == 3){
          printf(PURPLE "3 " RESET);
        } else if(mat[i][j].val == 4){
          printf(RED "4 " RESET);
        } else if(mat[i][j].val == 5){
          printf("5 ");
        } else if(mat[i][j].val == 6){
          printf("6 ");
        } else if(mat[i][j].val == 7){
          printf("7 ");
        } else if(mat[i][j].val == 8){
          printf("8 ");
        }
      } else if(mat[i][j].dis == 2){
        printf("🚩 ");
      } else if(mat[i][j].dis == 3){
        printf("💣 ");
      } else if(mat[i][j].dis == 4){
        printf("💥 ");
      }
    }
    printf("\n");
  }
}

void libera_celula(cell** mat, int a, int b, int n){
  if(mat[a][b].val == 0 && mat[a][b].dis != 1){
    mat[a][b].dis = 1;
    printf("done\n");
    /*leste*/
    if(b+1<n){
      libera_celula(mat, a, b+1, n);
    }
    /*oeste*/
    if(b-1>=0){
      libera_celula(mat, a, b-1, n);
    }
    /*sul*/
    if(a+1<n){
      libera_celula(mat, a+1, b, n);
    }
    /*sudeste*/
    if(a+1<n && b+1<n){
      libera_celula(mat, a+1, b+1, n);
    }
    /*sudoeste*/
    if(a+1<n && b-1>=0){
      libera_celula(mat, a+1, b-1, n);
    }
    /*norte*/
    if(a-1>=0){
      libera_celula(mat, a-1, b, n);
    }
    /*nordeste*/
    if(a-1>=0 && b+1<n){
      libera_celula(mat, a-1, b+1, n);
    }
    /*noroeste*/
    if(a-1>=0 && b-1>=0){
      libera_celula(mat, a-1, b-1, n);
    }
  } else {
    mat[a][b].dis = 1;
  }
}

int checa_vitória(cell** mat, int n){
  int vit = 1;
  for(int i=0; i<n && vit; i++){
    for(int j=0; j<n; j++){
      if(mat[i][j].val == 9 && mat[i][j].dis != 2){
        vit = 0;
        break;
      }
    }
  }
  return vit;
}

void game(cell** mat, int* cond, int n){
  int opcao;
  char x, y;
  printf("\nEscolha uma opção para jogar:\n");
  printf("1 - colocar/tirar uma bandeira\n");
  printf("2 - clicar numa célula\n\n");
  scanf("%d", &opcao);

  while (opcao != 1 && opcao != 2) {
    printf("Input não válido\n");
    printf("Escolha uma opção para jogar: ");
    scanf("%d", &opcao);
  }

  printf("Digite a coluna: ");
  scanf(" %c", &y);

  if (y < A || y > A+n-1) { // Caractere não representa uma coluna
    y -= A_LOWER - A; // Tenta deixar o caractere em maiúsculo
  }

  while (y < A || y > A+n-1) { // Caso ainda não represente uma coluna
    printf("Input não válido\n");
    printf("Digite a coluna: ");
    scanf(" %c", &y);

    if (y < A || y > A+n-1) // Caractere novo não representa uma coluna
      y -= A_LOWER - A; // Tenta deixar o caractere novo em maiúsculo
  }
 
  printf("Digite a linha: ");
  scanf(" %c", &x);

  if (x < A || x > A+n-1) { // Caractere não representa uma linha
    x -= A_LOWER - A; // Tenta deixar o caractere em maiúsculo
  }

  while (x < A || x > A+n-1) { // Caso ainda não represente uma linha
    printf("Input não válido\n");
    printf("Digite a linha: ");
    scanf(" %c", &x);

    if (x < A || x > A+n-1) // Caractere novo não representa uma linha
      x -= A_LOWER - A; // Tenta deixar o caractere novo em maiúsculo
  }

  // Conversão de letras em coordenadas
  x -= A;
  y -= A;

  switch(opcao){
    case 1:
      if(mat[x][y].dis == 1){
        printf("célula já foi mostrada");
      } else if(mat[x][y].dis == 2){
        //printf("esta coordenada já possui uma bandeira");
        mat[x][y].dis = 0;
      } else {
        mat[x][y].dis = 2;
        if(checa_vitória(mat, n) == 1){
          *cond = 2;
        }
      }
      break;
    default:
      if(mat[x][y].val == 9){
        *cond = 1;
      } else if(mat[x][y].dis == 2){
        printf("esta coordenada possui uma bandeira");
      } else if(mat[x][y].val != 0){
        mat[x][y].dis = 1;
      } else {
        /*mostre todos os lugares permitidos*/
        //mat[x][y].dis = 1;
        libera_celula(mat, x, y, n);
      }
      break;
  }
}

void criar_arquivo(char *nome, int segundos2, int minutos){
	FILE *fp;
	nome = strcat(nome,".csv");
	fp=fopen(nome,"w+");
  fprintf(fp,"Tempo de Jogo:%d minutos e %d segundos.", minutos,segundos2);
	fclose(fp);
}//Popula arquivo .csv

int main(){
  /*determine o tamanho do tabuleiro*/
  int n, cond=0;
  char nome[50]="teste";
  printf("Escolha um numero entre 10 e 20 para ser o tamanho do jogo: ");
  scanf("%d", &n);

  while(n>20||n<10){
    printf("O número escolhido não foi entre 10 e 20, por favor digite outro numero: ");
    scanf("%d", &n);
  }

  printf("você escolheu o numero %d\n", n);
  
  /*cria o jogo*/
  cell** mat = criar_jogo(n);

  /*marca o momento de início*/
  time_t instante1 = time(NULL);

  /*enquanto o jogo não acaba*/
  while(cond==0){
    system("clear");
    mostrar_tabuleiro(mat, n, cond);
    game(mat, &cond, n);
    //printf("quer sair? Digite 1: ");
    //scanf("%d", &cond);
  }
  system("clear");

  /*jogo acabou*/
  mostrar_tabuleiro(mat, n, cond);
  if(cond == 1){
    printf("\nVocê perdeu...\n");
  } else if(cond == 2){
    printf("\nVocê ganhou!\n");
  }
  /*marca o momento de fim*/
  time_t instante2 = time(NULL);

  /*calcula em segundos o tempo de jogo*/

  if (cond==2){// Cond ==2, 1 apenas para fins de teste
    int segundos = (int) (instante2 - instante1);

    /*transforma os segundos em minutos*/
    int minutos = segundos / 60;

    /*valor de segundos menor que 1 minuto*/
    int segundos2 = segundos % 60;

    printf("%d minutos e %d segundos\n",minutos, segundos2);
    
    printf("Digite o nome do Arquivo a ser Salvo\n");
    scanf("%s",&*nome);
    criar_arquivo(nome ,segundos2, minutos);
  }
  return 0;
}
