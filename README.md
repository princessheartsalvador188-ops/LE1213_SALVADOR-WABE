#include <stdio.h>
#include <string.h>

int main() {
    FILE *fp;
    int n, i, age;
    char name[50], course[50];
    char line[100];

    printf("How many student do you want to record? ");
    scanf("%d", &n);
    getchar(); 

    fp = fopen("student_records.txt", "w");
    if (fp == NULL) {
        printf("Cannot open file.\n");
        return 1;
    }

    for (i = 1; i <= n; i++) {
        printf("\nStudent %d\n", i);

        printf("Name: ");
        fgets(name, sizeof(name), stdin);
        name[strcspn(name, "\n")] = 0;

        printf("Age: ");
        scanf("%d", &age);
        getchar();

        printf("Course: ");
        fgets(course, sizeof(course), stdin);
        course[strcspn(course, "\n")] = 0;

        fprintf(fp, "Student %d\n", i);
        fprintf(fp, "Name: %s\n", name);
        fprintf(fp, "Age: %d\n", age);
        fprintf(fp, "Course: %s\n", course);

        fprintf(fp, "_____________________\n\n");
    }

    fclose(fp); 

    fp = fopen("student_records.txt", "r");
    if (fp == NULL) {
        printf("Cannot open file.\n");
        return 1;
    }

    printf("\nStudent Records:\n\n");
    while (fgets(line, sizeof(line), fp) != NULL) {
        printf("%s", line);
    }

    fclose(fp); 
    return 0;
}
