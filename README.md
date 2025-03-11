# chalangee

#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

typedef struct pile {
    int sommet;
    int taille;
    char pile[100];
} pile;

pile global_pile = {0, 100, {0}};

int my_strlen(const char *str) {
    int count = 0;
    while (*str != '\0') {
        count++;
        str++;
    }
    return count;
}

void reverse_string(char *str) {
    char *p1, *p2, temp;
    int size = my_strlen(str);

    for (p1 = str, p2 = str + (size - 1); p1 < p2; p1++, p2--) {
        temp = *p1;
        *p1 = *p2;
        *p2 = temp;
    }
}

void reverse_words(char str[]) {
    char *start = str, *end = str, *p;
    int size = my_strlen(str);

    reverse_string(str);

    while (*start != '\0') {
        while (*start == ' ') {
            start++;
        }
        end = start;
        while (*end != '\0' && *end != ' ') {
            end++;
        }
        char *p1, *p2, temp;
        for (p2 = end - 1, p1 = start; p1 < p2; p1++, p2--) {
            temp = *p1;
            *p1 = *p2;
            *p2 = temp;
        }
        start = end;
    }
}

int isempty(pile p) {
    return (p.sommet == 0);
}

int isfull(pile f) {
    return (f.sommet == f.taille);
}

char top(pile p) {
    return p.pile[p.sommet - 1];
}

void pop(pile *p) {
    if (!isempty(*p)) {
        --(p->sommet);
    } else {
        printf("Stack is empty!!\n");
    }
}

bool isValid(const char *s) {
    while (*s != '\0') {
        if (!isfull(global_pile)) {
            if ((*s == '(') || (*s == '[') || (*s == '{')) {
                global_pile.pile[(global_pile.sommet)++] = (*s);
            } else if ((*s == ')') || (*s == ']') || (*s == '}')) {
                if (!isempty(global_pile)) {
                    if ((top(global_pile) == '(' && *s == ')') ||
                        (top(global_pile) == '[' && *s == ']') ||
                        (top(global_pile) == '{' && *s == '}')) {
                        pop(&global_pile);
                    } else {
                        return false;
                    }
                } else {
                    return false;
                }
            }
        } else {
            printf("Stack is full\n");
            return false;
        }
        s++;
    }
    return ;
}

int main(void) {
    char test1[] = "edoc fo esuoH oT emocleW";

 char test2[] = "uoy pleh lliw ti ;3 melborp ni noitcnuf siht esU";
 char test3[] = "Hello World";
 char test4[] = "G";
 printf("Before: %s\n", test1);
 reverse_string(test1);
 printf("After: %s\n\n", test1);
 printf("Before: %s\n", test2);
 reverse_string(test2);
 printf("After: %s\n\n", test2);
 printf("Before: %s\n", test3);
 reverse_string(test3);
 printf("After: %s\n\n", test3);
 printf("Before: %s\n", test4);
 reverse_string(test4);
 printf("After: %s\n\n", test4);  printf("Is valid: %d\n", isValid(test4));

    return 0;
}
