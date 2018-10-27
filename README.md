# Gauss-Jordan-Reduction-Algorithm-in-C

#include <stdio.h>
#include <stdlib.h>

int column_red(int x, int y, int z);
void print_matx(int x, int y);
void read_int(const char* file_name, int x,int y);

//Memory for equation data
float eq[200][201] = {0.0};

//temporary variabel
float temp;


void header();

int main(void)
{
    int i,j,k,m;

    //number of equations
    int size = 0;
    //number of variabels in each equation
    int column = 0;

	header();
	system("pause");
    system("cls");
    printf("========================================\n");
    printf("                  MENU\n");
    printf("========================================\n\n");
    printf("[1] Run the Program \n[2] Help \n[3] Exit Program\n\n");
    printf("Pilih:");
    scanf("%d", &m);
    switch (m)
    {

    case 1://Run the Program Menu
    	system("cls");
    	printf("============================================\n");
   		printf("    	GAUSS JORDAN REDUCTION PROGRAM             \n");
    	printf("============================================\n\n");
   		//input the number of equations and variabel
   		printf(" Jumlah persamaan  : ");
  		scanf("%d", &size);
  		printf(" Jumlah variabel   : ");
   		scanf("%d", &column);
        //number of variabel + 1, get the number of column
   		column++;
   		printf("\n");

   		//input the data for each equations
        read_int("data.txt", size,column);

    	//display the matrix before reduction
   		printf(" Before Reduction:\n");
    	print_matx(size, column);

    		//gauss jordan operation
   		for( i=0; i<size; i++)
   		{
    		if(i==0)
   		    {
            column_red(i, column, size);
       		}
       		for( j=0; j<i; j++)
        	{
            	for( k=0; k<column; k++)
            	{
               		temp = eq[j][k];
              	 	eq[j][k] = eq[i][k];
              	 	eq[i][k] = temp;
            	}
            	if(j==0)
               		{
                   		column_red(i, column, size);
               		}
        	}
    	}
    	for( i=0; i<size; i++)
    	{
        	for( j=0; j<i; j++)
        	{
           		for( k=0; k<column; k++)
           		{
                	temp = eq[j][k];
                	eq[j][k] = eq[i][k];
                	eq[i][k] = temp;
            	}
        	}
   		}

   		//display matrix after reduction
    	printf(" After Reduction:\n");
        print_matx(size, column);

   		//display the solutions
    	printf("Solusi: \n");
    	int count =0;
    	for( i=0; i<size; i++)
    	{
    		for( j=0; j<column-1;j++)
    		{
    			count = count + eq[i][j];
			}
		}
		if(count==(column-1))
		{
    		for( i=0; i<size; i++)
    		{
        		printf("x%d = %.3f  ", i+1, eq[i][column-1]);
    		}
    	}
    	else
    	{
    		printf("Solusi tidak ada");
		}


    	printf("\n\n");
    	system("pause");
    	system("cls");
        return main();
    	break;
    case 2://Help Menu
    	system("cls");
    	printf("==============================================================================\n\n");
   		printf("    				HELP MENU              \n\n");
    	printf("==============================================================================\n\n");
    	printf("[1] In the main menu, select menu number 1 to run the program.\n\n");
    	printf("[2] Then you will be asked to determine how many equations you\n    have.\n\n");
    	printf("[3] Then you will be asked to determine the number of variables on\n    these equations.\n\n");
    	printf("[4] the number of equations and variables must be the same as the data in the file.\n\n");
    	printf("[5] You will get the Gauss reduction and the solution for your equation.\n\n");
    	printf("[6] If you want to exit the program, please select menu number 3 on the main\n    menu.\n\n");

    	printf("\n\n");
    	system("pause");
    	system("cls");
        return main();
    	break;
    case 3:
    	system("cls");
		printf("Thankyou\n\n");
		system("pause");
    	system("cls");
    	return 0;
    default :
		printf("Wrong Input !\n");
		printf("Input only the number of 1 to 3\n\n");
		system("pause");
		system("cls");
		return main();


	}
}

void print_matx(int x,int y)//x:size; y:column.
{
    int i,j;
    for( i=0; i<x; i++)
   		{
       		for( j=0; j<y; j++)
      		{
         		printf(" %3.3f  ", eq[i][j]);
        	}
       		 printf("\n\n");
   		}
}


//reduction fuction
int column_red(int x, int y, int z) // x=i(present column), y=column(number of columns), z=size(number of equations)
{
    float n;
    int i,j;
    n = eq[0][x];
    if(n==0)
    {
        return 1;
    }
    for( i=0; i<y; i++)
    {
        eq[0][i] = eq[0][i]/n;
    }

    for( i=0; i<z; i++)
    {
        n = eq[1+i][x];
        for( j=0; j<y; j++)
        {
            eq[1+i][j] = eq[1+i][j] - n*eq[0][j];
        }
    }
}

//read a data file fuction
void read_int(const char* file_name, int x,int y)//x:size; y:column
{
   FILE *myFile;
    myFile = fopen(file_name, "r");

    //read file into array
    int data[100]={0.0};
    int i,j;

    if (myFile == NULL){
        printf("Error Reading File\n");
        exit (0);
    }

    for (i = 0; i < x*y; i++){
        fscanf(myFile, "%d,", &data[i] );
    }

    fclose(myFile);

    for( i=0; i<x; i++)
    {
        for( j=0; j<y; j++)
        {
            eq[i][j] = data[j+i*y];
        }
    }

}

void header()
{
    printf("============================================================================\n");
    printf("\n                         GAUSS JORDAN REDUCTION                        \n\n");
    printf("============================================================================\n");
    printf("\n\nBy : Aqdam Zain Hajj & Muhammad Koku                    \n");
    printf("----------------------------------------------------------------------------\n");
    printf("\n\n\n");

}
