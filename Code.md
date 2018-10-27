# Project Title

Implementation Of Gaus Jordan Reduction in C

## Getting Started

This program is useful for someone who needs to solve many linear equations.

```
Give examples
```

### Table of Content

1.Read the file
2.Display the matrix
3.Gauss Jordan Reduction

### Read the text file code
```
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
```

### Display matrix Code
```
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
```

### Gauss Jordan Reduction Code
```
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
```

