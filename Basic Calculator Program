/*
 * Basic Calculator Program
 * Features: switch-case operation selection, loop until exit,
 *           modular functions per operation, input validation
 */

#include <stdio.h>

/* ---------- Function declarations ---------- */
float add(float a, float b);
float subtract(float a, float b);
float multiply(float a, float b);
int divide(float a, float b, float *result);  /* returns 0 on success, -1 on divide-by-zero */
int getValidNumber(const char *prompt, float *out);
char getValidOperator();

/* ---------- Function definitions ---------- */

float add(float a, float b) {
    return a + b;
}

float subtract(float a, float b) {
    return a - b;
}

float multiply(float a, float b) {
    return a * b;
}

int divide(float a, float b, float *result) {
    if (b == 0) {
        return -1; /* signal error, do not crash the program */
    }
    *result = a / b;
    return 0;
}

/* Reads a float safely. Keeps asking until the user gives a valid number.
   Returns 1 if user typed 'q' to quit mid-input, else 0. */
int getValidNumber(const char *prompt, float *out) {
    char buffer[100];
    while (1) {
        printf("%s", prompt);
        if (scanf("%99s", buffer) != 1) {
            /* clear bad input state */
            while (getchar() != '\n');
            continue;
        }
        if (buffer[0] == 'q' || buffer[0] == 'Q') {
            return 1;
        }
        /* try to parse the string as a float */
        char extra;
        if (sscanf(buffer, "%f%c", out, &extra) == 1) {
            return 0; /* clean parse, one float only, nothing left over */
        }
        printf("Invalid number. Please enter digits only (e.g. 12 or 3.5).\n");
    }
}

char getValidOperator() {
    char op;
    while (1) {
        printf("Choose operation (+, -, *, /): ");
        scanf(" %c", &op);
        if (op == '+' || op == '-' || op == '*' || op == '/') {
            return op;
        }
        printf("Invalid operator. Please enter one of + - * /\n");
    }
}

int main() {
    char choice;
    float num1, num2, result;
    int quit;

    printf("=== Simple Calculator ===\n");
    printf("(Type 'q' instead of a number at any time to exit)\n\n");

    while (1) {
        char op = getValidOperator();

        quit = getValidNumber("Enter first number: ", &num1);
        if (quit) break;

        quit = getValidNumber("Enter second number: ", &num2);
        if (quit) break;

        switch (op) {
            case '+':
                printf("Result: %.2f\n", add(num1, num2));
                break;
            case '-':
                printf("Result: %.2f\n", subtract(num1, num2));
                break;
            case '*':
                printf("Result: %.2f\n", multiply(num1, num2));
                break;
            case '/':
                if (divide(num1, num2, &result) == 0) {
                    printf("Result: %.2f\n", result);
                } else {
                    printf("Error: Division by zero is not allowed.\n");
                }
                break;
        }

        printf("\nDo another calculation? (y/n): ");
        scanf(" %c", &choice);
        if (choice == 'n' || choice == 'N') {
            break;
        }
        printf("\n");
    }

    printf("\nCalculator closed. Goodbye!\n");
    return 0;
}
