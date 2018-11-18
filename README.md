#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAXWORDS 100

void main(void)
{
FILE *fpin; // входной файл
FILE *fpout; // выходной файл
char word[32] = { NULL };
char allWords[MAXWORDS][32] = { NULL };
int stats[32] = { NULL };
int i = 0, count = 0, j;
fpin = fopen("test.txt", "rt"); // открыть файл для чтения
if (fpin == NULL)
return; // ошибка при открытии файла
fpout = fopen("result.txt", "wt"); // открыть файл для записи
if (fpout == NULL)
return; // ошибка при открытии файла
while (!feof(fpin))// цикл до конца входного файла
{
fscanf(fpin, "%s", word); // берет слово из файла
strcpy(allWords[i], word); // Добавляет слово в массив слов allWords
stats[strlen(word)-1]++; // В массиве Stats , увеличивает элемент равный длине слова
i++;
}
fclose(fpin); // закрыть входной файл
count = i; 
for (i = 1; i < count; i++) // Методом пузырька взависимости от длины слова сортируем массив слов allWords
for (j = 0; j < count - i; j++)
if (strlen(allWords[j]) > strlen(allWords[j + 1])) {
strcpy(word, allWords[j]);
strcpy(allWords[j], allWords[j + 1]);
strcpy(allWords[j + 1], word);
}
fpin = fopen("test.txt", "rt"); // открыть файл для чтения
for (i = 0; i < 32; i++) // Выводим статистику длинн слов
{
if (stats[i]) // выводим только те, где значение не 0
{
printf("%d slov dlini v [%d] symvol(ov)\n", stats[i], i + 1);
}
}
for (i = 0; i < count; i++) // Выводим слова в файл по возрастанию
{
fprintf(fpout, "%s\n", &(allWords[i]));
}
fclose(fpin); // закрыть входной файл
fclose(fpout); // закрыть выходной файл
system("pause");
}
