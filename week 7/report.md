# Week 7 Development Diary: Refining and Extending the Word Counter

## Overview

The seventh week was focused on bringing some much-needed functionality and structure to the word counter application. I tackled these tasks:

1. Implementing Sorting Methods
2. Adding Search Functionality
3. Parsing Command Line Arguments
4. Cleaning Up Words in the `addWord()` function

Here's a day-by-day breakdown of how the week unfolded.

---

### Sunday - Implementing Sorting Methods (`Dsort()` and `Asort()`)

The start of the week was dedicated to implementing sorting functionalities. Previously, the word map just accumulated words and their frequencies, without offering a way to sort this information.

I introduced two sorting functions (`Dsort()` for descending and `Asort()` for ascending) and a higher-level `sortWordsByCount()` function that decides which sort function to use based on a flag.

```c
//---------------------------------sorting methods-----------------------
int Dsort(const void *a, const void *b){
    //cast the void pointers into word pointers
    word *wordA = (word*)a;
    word *wordB = (word*)b;
    return wordB->count - wordA->count; //sorting in decending order
}

int Asort(const void *a, const void *b){
    //cast the void pointers into word pointers
    word *wordA = (word*)a;
    word *wordB = (word*)b;
    return wordA->count - wordB->count; //sorting in acending order 
}

void sortWordsByCount(wordMap *map, int op) {
  if(op==0){
    qsort(map->entries, map->size, sizeof(word), Dsort);
  }
  if(op==1){
    qsort(map->entries, map->size, sizeof(word), Asort);
  }

}

```

---

### Monday - Adding Search Functionality

Day 2 focused on providing a search functionality. I wanted the application to allow users to search for a specific word and see its frequency.

I implemented a binary search function named `searchMap()`, which calls `bsearch()`. Prior to searching, the word map is sorted alphabetically using a `compareWordsByWord()` function.

```c
//---------------------------------search methods-----------------------


//function to sort before  binary search
int compareWordsByWord(const void *a, const void *b) {
    word *wordA = (word *)a;
    word *wordB = (word *)b;
    return strncmp(wordA->word, wordB->word,50);  // Sort in ascending order based on the word
}


int wordCompare(const void *key, const void *element){
    const char *target= (const char *)key;
    word *wordElement = (word *)element;
    return strncmp(target , wordElement->word, 50);
}

// caseOpt==1 -> case sensitivty off
word* searchMap(const char *target , wordMap *map){
  qsort(map->entries, map->size, sizeof(word), compareWordsByWord);
  return (word*) bsearch(target, map->entries, map->size, sizeof(word), wordCompare);
}

```

---

### Tuesday - Parsing Command Line Arguments

After sorting and searching were implemented, it was time to handle them through command-line arguments. The goal was to allow users to specify flags for sorting (`-sa` for ascending, `-sd` for descending) and searching (`-f` for find).

The `main()` function was updated to parse `argc` and `argv` to accommodate these new options.

```c
 // Check if filename is provided 
    if (argc < 2 || argc > 4) {
        printf("Usage: %s <filename> [-sd|-sa]\nSearch Usage: %s <filename> [-f] [word_to_be_searched]\n", argv[0],argv[0]);
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

   //checking the sort flags entered
   if(argc==3 && strncmp(argv[2],"-sa",3)==0){
      sortWordsByCount(map,1); //do ascending sort
      printWordMap(map);  // Print the contents of the map

   }
 
  else  if(argc==3 && strncmp(argv[2],"-sd",3)==0){
      sortWordsByCount(map,0); //do decending sort
      printWordMap(map);  // Print the contents of the map

   }
//search without case sensitivty
  else if(argc==4 && strncmp(argv[2],"-f",2)==0){
          struct word *found = searchMap(argv[3],map);
          if  (found != NULL){
          printf("word found is %s, it was repeated %d times. ", found->word,found->count);
          }
          else{ 
          printf("word not found.");
          }
  }

  else{
      sortWordsByCount(map,0); //do decending sort by default
      printWordMap(map);  // Print the contents of the map

   }

```

---

### Wednesday - Cleaning Up Words with `cleanWord()`

The final major task was to improve how words are stored in the map. Until now, a word with special characters (like "hello!") would be treated differently than its clean form ("hello"). 

I implemented a `cleanWord()` function that strips non-alphabetic characters from a word. I then updated `addWord()` to call `cleanWord()` before storing or updating words in the map.

```c
//---------------------------------map methods-----------------------






void cleanWord(char *word) {
    int j = 0; // Create a variable 'j' for the cleaned word's index
    for (int i = 0; word[i] != '\0'; i++) {  // Loop through each character in the word
        if (isalpha(word[i])) {  // If the character is a letter, keep it
            word[j] = word[i];
            j++;  // Move 'j' to the next position
        }
      else if (i!=0) { break;} //break loop if a sympol is met after the first character.
    }
    word[j] = '\0';  // End the cleaned word with a null character
}


void addWord(wordMap *map, const char *newWord) {
    char cleanBuffer[50];  // Temporary buffer to hold the cleaned word
    strncpy(cleanBuffer, newWord, 49);  // Copy the new word into the buffer
    cleanBuffer[49] = '\0';  // Ensure null termination
    cleanWord(cleanBuffer);  // Clean the word using the cleanWord function
    
    // Search for the word in the map
    for (int i = 0; i < map->size; i++) {
        if (strcmp(map->entries[i].word, cleanBuffer) == 0) {
            // Word found, increment the count
            map->entries[i].count++;
          // printf("added word %s\n",cleanBuffer);
            return;  // Exit the function since the word was found
        }
    }

    // If the word was not found in the map, add it
    if (map->size < getMaxSize()) { // Ensure there's space in the map
        strncpy(map->entries[map->size].word, cleanBuffer, 49);  // Copy the cleaned word
        map->entries[map->size].word[49] = '\0';  // Ensure null termination
        map->entries[map->size].count = 1;  // Initialize count to 1
      //printf("created and added  %s\n",cleanBuffer);
        map->size++;  // Increase the size of the map
    } else {
        printf("Error: Word map is full!\n");
    }
}


```

---

### Thursday - Final Integration and Testing

On the last day, I integrated all the changes:

- Words are sorted based on the flags.
- Search functionality is active.
- Command-line arguments are successfully parsed.
- Words are cleaned before they are added to the map.

I conducted comprehensive tests to ensure that each feature was working as intended and debugged minor issues that cropped up.

---

By the end of Week 7, the word counter had evolved into a more robust, feature-complete application. It now allows for sorting by frequency, searching for specific words, and ensures that words are stored in a cleaned format. Future enhancements will include the following:
1. Sending output to files rather than standard output.
2. Using a linked list that is dynamically allocated.
3. Using heap less often unless necessary.
4. debugging using GDB
5. using Cmake to create the output files and manage the workflow.
