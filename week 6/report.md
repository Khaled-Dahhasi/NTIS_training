# Week 6 Development Diary: Implementing a Basic Word Counter

## Overview
This week, I embarked on the initial steps of creating a word counter application. This report outlines the development process, organized by the day. The code is written in C, and I've already set up the basic structure, including the `main` function, and additional functionalities such as word map creation, word addition, and word map printing.

### Sunday - `struct` Definitions and `createWordMap()`

On Sunday, I started by defining the basic `struct`s for storing individual words and the word map. 

- `struct word` contains a `char` array for the word itself and an `int` for the count.
- `struct wordMap` contains an array of `word` structures and an `int` for the size of the map.

```c
struct word {
    char word[50];
    int count;
};

struct wordMap {
    word entries[WORDMAP_MAX_SIZE];
    int size;
};

```

I also implemented `createWordMap()` to initialize an empty word map. This function allocates memory for the map and sets its size to zero.

```c
wordMap* createWordMap() {
    wordMap* map = (wordMap*) malloc(sizeof(wordMap));
    map->size = 0;
    return map;
}
```

### Monday - File Reading in `main()`

On Monday, I implemented the portion of the `main()` function responsible for file operations. This includes:

- Argument checks
- File opening
- Reading words into a temporary array

Here is the related code snippet:

```c
    FILE *file;
    char word[50];
    wordMap* map= createWordMap();

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
        //printf("%s\n", word);
    }


```

### Tuesday - Implementing `addWord()`

On Tuesday, I implemented the `addWord()` function. This function searches for a given word in the map and either updates its count or adds it if it's not already present. 

```c
void addWord(wordMap *map, const char *newWord) {
    // Search for the word in the map
    for (int i = 0; i < map->size; i++) {
        if (strcmp(map->entries[i].word, newWord) == 0) {
            // Word found, increment the count
            map->entries[i].count++;
           // printf("found word %s\n", newWord);
            return; // Exit the function since the word was found
        }
    }

    // If the word was not found in the map, add it
    if (map->size < getMaxSize()) { // Ensure there's space in the map
        strncpy(map->entries[map->size].word, newWord, 49);  // Copy the new word
        map->entries[map->size].word[49] = '\0';  // Ensure null termination
        map->entries[map->size].count = 1;  // Initialize count to 1
        map->size++;  // Increase the size of the map
        //printf("added word %s\n", newWord);
    } else {
        printf("Error: Word map is full!\n");
    }
}
```

### Wednesday - `printWordMap()` and Debugging

By Wednesday, I had enough functionality to test some outputs, so I implemented the `printWordMap()` function. This function iterates through the word map and prints each word along with its count.
I then integrated this into the `main()` function, allowing me to print the contents of the map for debugging purposes.

```c
void printWordMap(wordMap *map) {
    printf("\nWords in the map:\n");
    for (int i = 0; i < map->size; i++) {
        printf("%s: %d\n", map->entries[i].word, map->entries[i].count);
    }
}


//implementation in main()
printWordMap(map);  // Print the contents of the map

```


### Thursday - Final Integration and Testing

On Thursday, I focused on the final integration. This included:

- Adding a call to `createWordMap()` to initialize the word map.
- Incorporating `addWord()` within the word-reading loop in `main()`.
- Adding a call to `printWordMap()` to display the final word counts.

After these changes, I ran several tests to ensure that words were being read, added, and counted correctly. 

```c


//full main function
int main(int argc, char *argv[]) {
    FILE *file;
    char word[50];
    wordMap* map= createWordMap();

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
        //printf("%s\n", word);
    }

printWordMap(map);  // Print the contents of the map

    // Close the file
    fclose(file);
    free(map);
    return 0;
}
```

The week concluded with a fully functional, albeit basic, word counter application. This sets the stage for more advanced features like sorting and searching, which are planned for future development.
