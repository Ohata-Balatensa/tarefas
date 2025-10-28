#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>
	typedef struct carro {
	int reg_carro; // registro do carro
	char tipo; // [P]equeno, [M] dio ou [G]rande�
	char status; // [L]ivre ou [A]lugado
	}carro;
	typedef struct cliente {
	char CPF[13]; // CPF do cliente
	char nome[80]; // nome do cliente
	int num_reg; // numero do registro do carro
	int dias; // tempo de perman ncia - em dias�
	}cliente;
void aloca_carro(carro **pcar,int qcar);
void aloca_cliente(cliente **pcli,int qcli);
void cadastra_carro(carro *pcar,int qcar);
void cadastra_cliente(cliente *pcli,carro *pcar,int qcar);
void devolucao(cliente *pcli,int qcli,carro *pcar,int qcar);
int busca_carro(carro *pcar,int qcar,char tam);
int busca_CPF(cliente *pcli,int qcli,char *aux);
void mostra_carro(carro *pcar,int qcar);
void mostra_cliente(cliente *pcli, int qcli);
	main()
	{
		carro *car=NULL;
		cliente *cli=NULL;
		int op,cont=0,pos;
		aloca_carro(&car,15);
		cadastra_carro(car,15);
	do{
	system("cls");
	printf("\n[1]Locacao \n[2]Devolucao \n[3]Mostra Cliente\n[4]Fim \nOpcao: ");
	scanf("%i",&op);
	fflush(stdin);
	switch(op)
	{
		case 1: mostra_carro(car,15);
		aloca_cliente(&cli,cont+1);
		cadastra_cliente(cli+cont,car,15);
		cont++;
		break;
		case 2: devolucao(cli,cont,car,15);
		break;
		case 3: mostra_cliente(cli,cont);
		break;
	}
	}while(op!=4);
	}//main
void aloca_carro(carro **pcar,int qcar)
{
if((*pcar=(carro*)realloc(*pcar,qcar*sizeof(carro)))==NULL)
exit(1);
}//aloca_carro
void aloca_cliente(cliente **pcli,int qcli)
{
if((*pcli=(cliente*)realloc(*pcli,qcli*sizeof(cliente)))==NULL)
exit(1);
}//aloca_cliente
void cadastra_carro(carro *pcar,int qcar)
{
int i;
for(i=0;i<qcar;i++,pcar++)
{
pcar->reg_carro=i+1;
pcar->status='L';
if(i<5) //5 carros pequenos
pcar->tipo='P';
else if(i<10) //5 carros medios
pcar->tipo='M';
else
pcar->tipo='G'; //5 carros grandes
}
}//cadastra_carro
void cadastra_cliente(cliente *pcli,carro *pcar,int qcar)
{
char tipcar;
int numcar;
printf("\nTipo de carro [P - M - G]: ");
scanf("%c",&tipcar);
fflush(stdin);
tipcar=toupper(tipcar);
numcar=busca_carro(pcar,qcar,tipcar);
if(numcar==-1)
printf("\nNao ha carros disponiveis desse tipo\n\n\n");
else
{
pcli->num_reg=numcar;
printf("\nCPF: ");
gets(pcli->CPF);
fflush(stdin);
printf("\nNome: ");
gets(pcli->nome);
fflush(stdin);
printf("\nQtos dias: ");
scanf("%i",&(pcli->dias));
fflush(stdin);
printf("\nCadastro feito com sucesso\nCarro: %i\n\n\n",pcli->num_reg);
}
system("pause");
}//cadastra_cliente
void devolucao(cliente *pcli,int qcli,carro *pcar,int qcar)
{
char aux_cpf[13],aux_tipo;
int pos,aux_reg,tempo;
printf("\nCPF a ser encerrado: ");
gets(aux_cpf);
fflush(stdin);
pos=busca_CPF(pcli,qcli,aux_cpf);
if(pos==-1)
printf("\nCPF invalido\n");
else
{
(aux_reg=(pcli+pos)->num_reg); //atribui para reg o n mero�
do carro
((pcar+aux_reg-1)->status='L'); //atualiza status para [L]ivre
(aux_tipo=(pcar+aux_reg-1)->tipo); //atribui para aux_tipo o tipo do
carro
(tempo=(pcli+pos)->dias); //atribui para tempo os dias de
aluguel
printf("\nNome: %s\nRegistro Carro: %i\nTipo Carro: %c\nDias: %i",(pcli+pos)-
>nome,aux_reg,aux_tipo,tempo);
switch(aux_tipo)
{
case 'P': printf("\nValor a pagar: %.2f\n\n",tempo*150.00);
break;
case 'M': printf("\nValor a pagar: %.2f\n\n",tempo*200.00);
break;
case 'G': printf("\nValor a pagar: %.2f\n\n",tempo*250.00);
break;
}//switch
}//else
system("pause");
}//devolucao
int busca_carro(carro *pcar,int qcar,char tam)
{
int i;
for(i=0;i<qcar;i++,pcar++)
if(pcar->tipo==tam && pcar->status=='L')
{
pcar->status='A';
return(pcar->reg_carro);
}
return -1;
}//busca_carro
int busca_CPF(cliente *pcli,int qcli,char *aux)
{
int i;
for(i=0;i<qcli;i++)
if(strcmp((pcli+i)->CPF,aux)==0)
return i;
return -1;
}//busca_CPF
void mostra_carro(carro *pcar,int qcar)
{
int i;
for(i=0;i<qcar;i++,pcar++)
printf("\nRegistro Carro: %i\nTipo: %c\nStatus: %c\n\n",pcar->reg_carro,pcar-
>tipo,pcar->status);
printf("\n\n\n");
system("pause");
}//mostra_carro
void mostra_cliente(cliente *pcli,int qcli)
{
int i;
for(i=0;i<qcli;i++,pcli++)
printf("\nCPF: %s\nNome: %s\nRegistro Carro: %i\nDias: %i\n\n",pcli->CPF,pcli-
>nome,pcli->num_reg,pcli->dias);
printf("\n\n\n");
system("pause");
}//mostra_client
