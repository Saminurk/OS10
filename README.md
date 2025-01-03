# OS10
#include <stdio.h>

#define MAX_BLOCKS 5
#define MAX_PROCESSES 4

// Function to implement the First Fit memory allocation
void firstFit(int blockSize[], int m, int processSize[], int n) {
    // Stores block id of the allocated block for each process
    int allocation[n];
    
    // Initially, no block is allocated
    for (int i = 0; i < n; i++) {
        allocation[i] = -1;
    }

    // Find a block for each process
    for (int i = 0; i < n; i++) {
        // Search for a block that can accommodate the process
        for (int j = 0; j < m; j++) {
            if (blockSize[j] >= processSize[i]) {
                // Allocate block j to process i
                allocation[i] = j;
                // Reduce the available memory in the block
                blockSize[j] -= processSize[i];
                break;
            }
        }
    }

    // Print the allocation result
    printf("Process No.\tProcess Size\tBlock No.\tBlock Size\n");
    for (int i = 0; i < n; i++) {
        if (allocation[i] != -1) {
            printf("%d\t\t%d\t\t%d\t\t%d\n", i + 1, processSize[i], allocation[i] + 1, blockSize[allocation[i]]);
        } else {
            printf("%d\t\t%d\t\tNot Allocated\n", i + 1, processSize[i]);
        }
    }
}

int main() {
    int blockSize[MAX_BLOCKS] = {100, 500, 200, 300, 600}; // Available memory blocks
    int processSize[MAX_PROCESSES] = {212, 417, 112, 426}; // Process sizes

    int m = sizeof(blockSize) / sizeof(blockSize[0]);
    int n = sizeof(processSize) / sizeof(processSize[0]);

    // Call firstFit function
    firstFit(blockSize, m, processSize, n);

    return 0;
}
