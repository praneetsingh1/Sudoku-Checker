/*
 ============================================================================
 Name        : sudoku.c
 Author      : Praneet Singh
 Version     :
 
 Description : Sudoku puzzle solution check
 ============================================================================
 */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <stdint.h>
#include <inttypes.h>
#define NUM_THREADS 10

//struct defines the row, column and index for each thread
typedef struct{
	int row;
	int column;
	int index;
} parameters;

int valid = 0; //used to check validity of all the values in the array
int isValid[11] = {0};	// Array contains either 0(condition not met) or 1(condition met) for all the threads.

//Initiate the grid
int grid[9][9] = {
			{6,5,3,1,2,8,7,9,4},
			{1,7,4,3,5,9,6,8,2},
			{9,2,8,4,6,7,5,3,1},
			{2,8,6,5,1,4,3,7,9},
			{3,9,1,7,8,2,4,5,6},
			{5,4,7,6,9,3,2,1,8},
			{8,6,5,2,3,1,9,4,7},
			{4,1,2,9,7,5,8,6,3},
			{7,3,9,8,4,6,1,2,5}
	};
	//Check the columns for repeated value, values are stored in seen array, if value has already been seen
	//column will be inValid.
	void *checkColumns(void *arg){
		parameters* args = (parameters*) arg;
		int row = args->row;
		int column = args->column;
		int index = args->index;
		for(int i = row; i < 9; i++){
			int seen[9] = {0};		//initiate an array to 0 after checking each column
			for(int j = column; j < 9; j++ ){
				int k = grid[i][j];
				if(seen[k-1] == 0){
					seen[k-1] = 1;


				} else{
					isValid[index] = 0;
					return (void*) 0;

				}
			}
		}
		isValid[index] = 1;
		return (void*) 0;
	}
	//Check the rows for repeated value, values are stored in seen array, if value has already been seen
		//row will be inValid.
	void *checkRows(void *arg){
		parameters* args = (parameters*) arg;
				int row = args->row;
				int column = args->column;
				int index = args->index;
				for(int i = column; i < 9; i++){
					int seen[9] = {0};		//initiate an array to 0 after checking each row
					for(int j = row; j < 9; j++ ){
						int k = grid[j][i];
						if(seen[k-1] == 0){
							seen[k-1] = 1;
						} else{
							isValid[index] = 0;
							return (void*) 0;
						}
					}
				}
				isValid[index] = 1;
				return (void*) 0;
		}
	// check a 3x3 section of the sudoku solution.
	void *checkCube(void *arg){
		parameters* args = (parameters*) arg;
						int row = args->row;
						int column = args->column;
						int index = args->index;
						int seen[9] = {0};		//array initiated to 0 per 3x3 cube
						for(int i = column; i < column+3; i++){
							for(int j = row; j < row+3; j++){
								int k = grid[i][j];
								if(seen[k-1] == 0){
									seen[k-1] = 1;
								} else{
									isValid[index] = 0;
									return (void*) 0;
								}
							}
						}
						isValid[index] = 1;
						return (void*) 0;
		}

int main(void) {
	//Start the initial values for rows and columns for different cases

	parameters *columnCheck = (parameters *) malloc(sizeof(parameters));
				columnCheck->row = 0;
				columnCheck->column = 0;
				columnCheck->index = 0;

	parameters *rowCheck = (parameters *) malloc(sizeof(parameters));
				rowCheck->row = 0;
				rowCheck->column = 0;
				rowCheck->index = 1;

	//Starting index of the 9 3x3 sections of the Sudoku puzzle
	parameters *cube1 = (parameters *) malloc(sizeof(parameters));
				cube1->row = 0;
				cube1->column = 0;
				cube1->index = 2;


	parameters *cube2 = (parameters *) malloc(sizeof(parameters));
				cube2->row = 0;
				cube2->column = 3;
				cube2->index = 3;

	parameters *cube3 = (parameters *) malloc(sizeof(parameters));
				cube3->row = 0;
				cube3->column = 6;
				cube3->index = 4;

	parameters *cube4 = (parameters *) malloc(sizeof(parameters));
				cube4->row = 3;
				cube4->column = 0;
				cube4->index = 5;

	parameters *cube5 = (parameters *) malloc(sizeof(parameters));
				cube5->row = 3;
				cube5->column = 3;
				cube5->index = 6;

	parameters *cube6 = (parameters *) malloc(sizeof(parameters));
				cube6->row = 3;
				cube6->column = 6;
				cube6->index = 7;

	parameters *cube7 = (parameters *) malloc(sizeof(parameters));
				cube7->row = 6;
				cube7->column = 0;
				cube7->index = 8;

	parameters *cube8 = (parameters *) malloc(sizeof(parameters));
				cube8->row = 6;
				cube8->column = 3;
				cube8->index = 9;

	parameters *cube9 = (parameters *) malloc(sizeof(parameters));
				cube9->row = 6;
				cube9->column = 6;
				cube9->index = 10;

	//set up the threads
	pthread_t threads[NUM_THREADS];

	// create threads
	pthread_create(&threads[0], NULL, checkColumns, columnCheck);
	pthread_create(&threads[1], NULL, checkRows, rowCheck);
	pthread_create(&threads[2], NULL, checkCube, cube1);
	pthread_create(&threads[3], NULL, checkCube, cube2);
	pthread_create(&threads[4], NULL, checkCube, cube3);
	pthread_create(&threads[5], NULL, checkCube, cube4);
	pthread_create(&threads[6], NULL, checkCube, cube5);
	pthread_create(&threads[7], NULL, checkCube, cube6);
	pthread_create(&threads[8], NULL, checkCube, cube7);
	pthread_create(&threads[9], NULL, checkCube, cube8);
	pthread_create(&threads[10], NULL, checkCube, cube9);

	//Wait for the threads
	//Takes the argument of the thread and a void**result
	for(int u = 0; u < NUM_THREADS; u++){
		pthread_join(threads[u], NULL);
	}
	//free the malloc
	free(columnCheck);
	free(rowCheck);
	free(cube1);
	free(cube2);
	free(cube3);
	free(cube4);
	free(cube5);
	free(cube6);
	free(cube7);
	free(cube8);
	free(cube9);


	printf("CS149 Sudoku from Praneet Singh\n");
	//Print the puzzle
	for(int p = 0; p < 9; p++){
		printf("\n");
		for(int k = 0; k < 9; k++){
				printf("%d ", grid[p][k]);
			}
		}
	//Solution can only be valid if all 11 threads' corresponding value in the array is 1.
	for(int s = 0; s < 11; s++){
		valid += isValid[s];
	}
		//Check if puzzle is valid. It will only be valid if all 11 threads are successful.
	if(valid == 11){
		printf("\nSudoku is valid!\n");
	}else{
		printf("\nSudoku is not valid!\n");
	}
}



