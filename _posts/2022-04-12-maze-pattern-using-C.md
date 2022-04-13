---
title: How to print a maze-looking pattern using C
excerpt_separator: <!--end_excerpt-->
---

Here is how you can print a random maze-looking pattern using C.

<!--end_excerpt-->

```C
#include <stdio.h>
#include <stdlib.h>
#include <sys/ioctl.h>
#include <time.h>
#include <unistd.h>

void draw_diagnonal_lines(int count) {
  for (int i = 0; i < count; i++) {
    if (rand() % 2 == 0) {
      printf("╱");
    } else {
      printf("╲");
    }
  }
}

void draw_orizonal_lines(int count) {
  for (int i = 0; i < count; i++)
    printf("─");
}

int main(void) {
  struct winsize w;
  ioctl(STDOUT_FILENO, TIOCGWINSZ, &w);

  printf("lines %d\n", w.ws_row);
  printf("columns %d\n", w.ws_col);

  printf("┌");
  draw_orizonal_lines(w.ws_col - 2);
  printf("┐\n");

  srand(time(NULL));
  for (int line = 0; line < w.ws_row - 3; line++) {
    printf("│");
    draw_diagnonal_lines(w.ws_col - 2);
    printf("│");

    puts("");
    // sleep(1);
  }

  printf("└");
  draw_orizonal_lines(w.ws_col - 2);
  printf("┘\n");

  return 0;
}
```
