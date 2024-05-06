# Ex-10-IMPLEMENTATION-OF-SIMPLE-CODE-OPTIMIZATION-TECHNIQUES
IMPLEMENTATION OF SIMPLE CODE OPTIMIZATION TECHNIQUES 
# Date: 05/04/2024
# Aim:
To write a C program to implement simple code optimization techniques such as Common subexpression elimination and Dead Code elimination.
# ALGORITHM :
1. Start the program.
2. The ‘L’values and their corresponding ‘R’ values are given as input.
3. After common subexpression elimination, the subexpressions that are common are identified and are removed.
4. After Dead code elimination, the subexpression that is of no use can be identified and is eliminated.
5. Stop the program.
# PROGRAM
```
#include <stdio.h>
#include <string.h>

struct op {
    char l;
    char r[20];
} op[10], pr[10];

int main() {
    int a, i, k, j, n, z = 0, m, q;
    char *p, *l;
    char temp, t;
    char *tem;

    printf("Enter the Number of Values: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("left: ");
        scanf(" %c", &op[i].l); // Notice the space before %c to consume the newline character
        printf("\tright: ");
        scanf("%s", op[i].r);
    }

    printf("Intermediate Code\n");
    for (i = 0; i < n; i++) {
        printf("%c=%s\n", op[i].l, op[i].r);
    }

    for (i = 0; i < n - 1; i++) {
        temp = op[i].l;
        for (j = 0; j < n; j++) {
            p = strchr(op[j].r, temp);
            if (p) {
                pr[z].l = op[i].l;
                strcpy(pr[z].r, op[i].r);
                z++;
            }
        }
    }

    pr[z].l = op[n - 1].l;
    strcpy(pr[z].r, op[n - 1].r);
    z++;

    printf("\nAfter Dead Code Elimination\n");
    for (k = 0; k < z; k++) {
        printf("%c\t=%s\n", pr[k].l, pr[k].r);
    }

    for (m = 0; m < z; m++) {
        tem = pr[m].r;
        for (j = m + 1; j < z; j++) {
            p = strstr(tem, pr[j].r);
            if (p) {
                t = pr[j].l;
                pr[j].l = pr[m].l;
                for (i = 0; i < z; i++) {
                    l = strchr(pr[i].r, t);
                    if (l) {
                        a = l - pr[i].r;
                        printf("pos: %d", a);
                        pr[i].r[a] = pr[m].l;
                    }
                }
            }
        }
    }

    printf("Eliminate Common Expression\n");
    for (i = 0; i < z; i++) {
        printf("%c=%s\n", pr[i].l, pr[i].r);
    }

    for (i = 0; i < z; i++) {
        for (j = i + 1; j < z; j++) {
            q = strcmp(pr[i].r, pr[j].r);
            if ((pr[i].l == pr[j].l) &&!q) {
                pr[i].l = '\0';
                strcpy(pr[i].r, "\0");
            }
        }
    }

    printf("Optimized Code\n");
    for (i = 0; i < z; i++) {
        if (pr[i].l!= '\0') {
            printf("%c=%s\n", pr[i].l, pr[i].r);
        }
    }

    return 0;
}
```
# OUTPUT
![image](https://github.com/NAGINENIROHITH/Ex-10-IMPLEMENTATION-OF-SIMPLE-CODE-OPTIMIZATION-TECHNIQUES/assets/118344049/83c1f705-964c-4c94-a7d1-35f804c5a994)

# RESULT
The simple code optimization techniques such as common subexpression elimination and dead code elimination are implemented successfully and the output is verified.
