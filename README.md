#include <stdio.h>
#include <stdlib.h>

int grid[9][9];

int startIndex(int x){
    return 3*(x/3);
}

int canassign(int grid[9][9],int rowIndex,int colIndex,int num){
    for(int i=0;i<9;i++)
        if(grid[rowIndex][i]==num || grid[i][colIndex]==num)
            return 0;
    int x=startIndex(rowIndex),y=startIndex(colIndex);
    for(int i=x;i<x+3;i++){
        for(int j=y;j<y+3;j++){
            if(grid[i][j]==num)
                return 0;
        }
    }
    return 1;
}

int findunvisited(int grid[9][9],int *row,int *col){
    for(*row=0;*row<9;(*row)++){
        for(*col=0;*col<9;(*col)++){
            if(grid[*row][*col]==0){
                return 1;
            }
        }
    }
    return 0;
}

void print(int grid[9][9]){
    for(int i=0;i<9;i++,printf("\n"))    
        for(int j=0;j<9;j++)
            printf("%d ",grid[i][j]);
    printf("\n");
}

int solvesudoku(int grid[9][9]){
    int row,col;
    if(!findunvisited(grid,&row,&col)){
        return 1;
    }
    for(int num=1;num<=9;num++){
        if(canassign(grid,row,col,num)){
            grid[row][col]=num;
            if(solvesudoku(grid)){
                return 1;
            }
            grid[row][col]=0;
        }
    }
    return 0;
}


int main()
{
    for(int i=0;i<9;i++)    
        for(int j=0;j<9;j++)
            scanf("%d",&grid[i][j]);
    printf("\n");
    if(solvesudoku(grid))
        print(grid);
    else
        printf("CANNOT BE SOLVED");
}

/*
Test Case:

0 9 1 2 0 0 8 3 0
0 0 0 0 0 6 0 0 0
0 2 0 0 0 9 0 4 7
0 5 0 0 0 3 0 8 0
6 0 0 4 1 0 0 0 0
1 0 0 8 0 0 0 9 5
0 6 0 9 0 0 0 2 0
0 0 2 3 0 0 0 0 4
8 3 0 0 4 0 1 6 0

*/
