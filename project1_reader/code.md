# Reader C Program

## reader.c:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "reader.h"

struct wordMap* createWordMap() {
    struct wordMap* map = (struct wordMap*) malloc(sizeof(struct wordMap));
    map->size = 0;
    return map;
}

void addWord(struct wordMap *map, const char *newWord) {
    // Search for the word in the map
    for (int i = 0; i < map->size; i++) {
        if (strcmp(map->entries[i].word, newWord) == 0) {
            // Word found, increment the count
            map->entries[i].count++;
            printf("found word %s\n", newWord);
            return; // Exit the function since the word was found
        }
    }

    // If the word was not found in the map, add it
    if (map->size < getMaxSize()) { // Ensure there's space in the map
        strncpy(map->entries[map->size].word, newWord, 49);  // Copy the new word
        map->entries[map->size].word[49] = '\0';  // Ensure null termination
        map->entries[map->size].count = 1;  // Initialize count to 1
        map->size++;  // Increase the size of the map
        printf("added word %s\n", newWord);
    } else {
        printf("Error: Word map is full!\n");
    }
}

void printWordMap(struct wordMap *map) {
    printf("\nWords in the map:\n");
    for (int i = 0; i < map->size; i++) {
        printf("%s: %d\n", map->entries[i].word, map->entries[i].count);
    }
}

int main(int argc, char *argv[]) {
    FILE *file;
    char word[50];
    struct wordMap* map= createWordMap();

    // Check if filename is provided
    if (argc != 2) {
        printf("Usage: %s <filename>\n", argv[0]);
        return 1;
    }

    // Open the file
    file = fopen(argv[1], "r");
    if (file == NULL) {
        perror("Error opening file");
        return 2;
    }

    // Read words from the file
    while (fscanf(file, "%49s", word) == 1) {
        addWord(map, word);
        printf("%s\n", word);
    }

    printWordMap(map);  // Print the contents of the map

    // Close the file
    fclose(file);
    free(map);
    return 0;
}




## reader.h:

```c
#include <stdlib.h>
#define WORDMAP_MAX_SIZE 1000000

struct word {
    char word[50];
    int count;
};

struct wordMap {
    struct word entries[WORDMAP_MAX_SIZE];
    int size;
};

void addWord(struct wordMap *map, const char *newWord);

void printWordMap(struct wordMap *map);

long int getMaxSize() {
    return WORDMAP_MAX_SIZE;
}

