# Ex-5 Rail-Fence-Program
### NAME:Swetha D
### Reg no:212223040222
# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM

```

#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// Function to encrypt the plaintext using Rail Fence Cipher
void encryptRailFence(char* text, int key) {
    int len = strlen(text);
    char rail[key][len];

    // Fill the rail matrix with '\n'
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    // Fill the rail matrix in zigzag
    int row = 0;
    int dir_down = 0; // direction flag
    for (int i = 0; i < len; i++) {
        rail[row][i] = text[i];

        if (row == 0 || row == key - 1)
            dir_down = !dir_down;

        row += dir_down ? 1 : -1;
    }

    // Collect the encrypted text
    printf("Encrypted Text: ");
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                printf("%c", rail[i][j]);

    printf("\n");
}

// Function to decrypt the cipher using Rail Fence Cipher
void decryptRailFence(char* cipher, int key) {
    int len = strlen(cipher);
    char rail[key][len];

    // Fill the rail matrix with '\n'
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    // Mark the zigzag pattern
    int row = 0;
    int dir_down = 0;
    for (int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if (row == 0 || row == key - 1)
            dir_down = !dir_down;

        row += dir_down ? 1 : -1;
    }

    // Fill the marked positions with cipher characters
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    // Now read the matrix in zigzag to construct the original text
    row = 0;
    dir_down = 0;

    printf("Decrypted Text: ");
    for (int i = 0; i < len; i++) {
        printf("%c", rail[row][i]);

        if (row == 0 || row == key - 1)
            dir_down = !dir_down;

        row += dir_down ? 1 : -1;
    }

    printf("\n");
}

int main() {
    char text[100];
    int key;

    printf("Enter the text: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0'; // Remove newline

    printf("Enter the key (number of rails): ");
    scanf("%d", &key);

    encryptRailFence(text, key);

    printf("\nNow enter encrypted text for decryption: ");
    char cipher[100];
    scanf("%s", cipher); // assuming no spaces

    decryptRailFence(cipher, key);

    return 0;
}
```

# OUTPUT
![{F6848BE3-F641-418E-B3C2-B6778284A891}](https://github.com/user-attachments/assets/31335c9b-aae4-4b86-a9a5-4aa46c0daeb5)

# RESULT
Thus the program is executed and the output is verified.
