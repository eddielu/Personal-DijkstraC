/****************************************************************
 *
 *
 *
 ****************************************************************/

 #include<stdio.h>
 #include<stdlib.h>

/* Free the Matrix of a given size */
static void freeMatrix(int **pColumn, int iSize) {
	int i;

	for (i = 0; i < iSize; i++) {
		free(pColumn[i]);
	}

	free(pColumn);

}

/* Set up the Matrix with a given size*/
static int** setupMatrix(char *sLength, int *iArraySize) {
 	int **pColumn;
 	int **pMaster;
 	int *pRow;
 	int i;
 	int index, node, length, result;

 	/* Create an empty matrix of appropriate size */
 	sscanf(sLength, "%d", iArraySize);
 	pColumn = (int **) calloc(*iArraySize, 4);
 	for (i = 0; i < *iArraySize; i++) {
 		pColumn[i] = (int *) calloc(*iArraySize, 4);
 	}

 	pMaster = pColumn;

 	/*Fill the matrix out with data */
 	result = scanf("%d,%d", &node, &length);
 	while (result > 0) {
 		node--;

 		if (result == 1) {
 			index = node;
 		}

 		else if (result == 2) {
 			pRow = pMaster[index];
 			pRow[node] = length;
 		}

 		result = scanf("%d,%d", &node, &length);
 	}


 	return pMaster;
}

/* Print Matrix in similar format to text file */
static void printMatrix(int **pMaster, int iSize) {
	int i, j;
	int *pRow;

	for (i = 0; i < iSize; i++) {
		printf("%d\t", i);
		pRow = pMaster[i];

		for (j = 0; j < iSize; j++) {
			if (pRow[j] != 0)
				printf("%d,%d\t", j, pRow[j]);
		}
		printf("\n");
		fflush(stdout);

	}
}

/* Set all values of iDistRecord to -1 */
static void clearRecord(int *iDistRecord, int iArraySize) {
	int i;

	for (i = 0; i < iArraySize; i++) {
		iDistRecord[i] = -1;
	}

	return;
}

/* Is iNode in X? */
static int isUnexplored(int *iDistRecord, int iNode) {
	return iDistRecord[iNode] == -1;
}

/* Return the node with smallest score from iXNode */
static int grabSmallestScore(int **pMaster, int iXNode, int iArraySize, int *iDistRecord) {
	int *pRow;
	int iMinVal = 9999;
	int iMinIndex = -1;
	int i;

	pRow = pMaster[iXNode];

	for (i = 0; i < iArraySize; i++) {
		if ((pRow[i] != 0) && (iMinVal > pRow[i]) && (isUnexplored(iDistRecord, i))) {
			iMinVal = pRow[i];
			iMinIndex = i;
		}
	}
	printf("%s", pRow[iMinIndex]);
	return pRow[iMinIndex];
}

/* Returns next node to add to X */
static int grabNextNode(int **pMaster, int *iDistRecord, int iArraySize) {
	int i;
	int iMinNode = -1;
	int iMinScore = 9999;
	int iNodeScore;

	for (i = 0; i < iArraySize; i++) {

		if (!isUnexplored(iDistRecord, i)) {

			iNodeScore = grabSmallestScore(pMaster, iDistRecord[i], iArraySize, iDistRecord);
			if (iMinScore > iNodeScore) {
				iMinScore = iNodeScore;
				iMinNode = i;
			}
		}
	}

	return iMinNode;

}

/* Main Dijkstra Function. Returns smallest distance. */
static int runDijkstra(int **pMaster, int iEnd, int iArraySize) {
	int *iDistRecord;

	iDistRecord = (int *) calloc(iArraySize, 4);
	clearRecord(iDistRecord, iArraySize);
	iDistRecord[0] = 0;

	while (1 == 1) {
		if (grabNextNode(pMaster, iDistRecord, iArraySize) == iEnd)
			break;
	}

	iEnd = iDistRecord[iEnd];


	free(iDistRecord);

	return iEnd;


}



 int main(int argc, char *argv[]) {
	int **pMaster;
	int *pRow;
	int iArraySize;
	int iResult;



	pMaster = setupMatrix(argv[1], &iArraySize);



	iResult = runDijkstra(pMaster, 3, iArraySize);
	printf("%d", iResult);

 	

 	freeMatrix(pMaster, iArraySize);


 	return 0;
 }
