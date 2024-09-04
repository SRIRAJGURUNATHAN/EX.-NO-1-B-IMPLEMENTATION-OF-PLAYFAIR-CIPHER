# EX.-NO-1-B-IMPLEMENTATION-OF-PLAYFAIR-CIPHER

## AIM:
  To write a C program to implement the Playfair Substitution technique.
  
## ALGORITHM:

STEP-1: Read the plain text from the user.

STEP-2: Read the keyword from the user.

STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.

STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.

STEP-5: Display the obtained cipher text.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

void matrixMultiplication(unsigned int res[], unsigned int mat[3][3], unsigned int vec[], int size) {
    int i, j;
    for (i = 0; i < 3; i++) {
        res[i] = 0;
        for (j = 0; j < 3; j++) {
            res[i] += mat[i][j] * vec[j];
        }
        res[i] = res[i] % 26; // Ensure result is within alphabet bounds
    }
}

int main() {
    unsigned int a[3][3] = { {6, 24, 1}, {13, 16, 10}, {20, 17, 15} }; // Encryption key
    unsigned int b[3][3] = { {8, 5, 10}, {21, 8, 21}, {21, 12, 8} }; // Decryption key
    int i, len;
    unsigned int c[20], d[20];
    char msg[20];
    
    printf("Enter plain text: ");
    scanf("%s", msg);
    
    len = strlen(msg);
    
    // Ensure the message length is a multiple of 3 by padding with 'X'
    while (len % 3 != 0) {
        msg[len++] = 'X';
    }
    msg[len] = '\0'; // Null terminate the string
    
    printf("Padded plain text: %s\n", msg);
    
    // Convert plaintext to numerical values (A=0, B=1, ..., Z=25)
    for (i = 0; i < len; i++) {
        c[i] = msg[i] - 'A';
    }
    
    // Encrypt the message in blocks of 3 characters
    printf("\nEncrypted Cipher Text :");
    for (i = 0; i < len; i += 3) {
        matrixMultiplication(d, a, &c[i], 3);
        for (int j = 0; j < 3; j++) {
            printf(" %c", d[j] + 'A');
        }
    }
    
    // Decrypt the message in blocks of 3 characters
    printf("\nDecrypted Cipher Text :");
    for (i = 0; i < len; i += 3) {
        matrixMultiplication(c, b, &d[i], 3);
        for (int j = 0; j < 3; j++) {
            printf(" %c", c[j] + 'A');
        }
    }
    
    return 0;
}

```


## OUTPUT:
![image](https://github.com/user-attachments/assets/0a8bce4f-5d42-4d76-b45c-304548ec6971)


## RESULT:
  Thus the Playfair cipher substitution technique had been implemented successfully.
