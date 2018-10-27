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
