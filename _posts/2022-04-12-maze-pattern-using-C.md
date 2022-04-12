---
title: How to print a maze-looking pattern using C
excerpt_separator: <!--end_excerpt-->
---

Here is how you can print a random maze-looking pattern using C.

<!--end_excerpt-->

```C
#include <stdio.h>
#include <time.h>
#include <stdlib.h>
#include <sys/ioctl.h>
#include <unistd.h>

int main(void)
{
	struct winsize w;
    ioctl(STDOUT_FILENO, TIOCGWINSZ, &w);

    printf ("lines %d\n", w.ws_row);
    printf ("columns %d\n", w.ws_col);

   	printf("┌");
    for(int i = 0; i < w.ws_col - 2; i++) {
    	printf("─");
    }
    printf("┐");
    int width = w.ws_col - 2;

	srand(time(NULL));
	printf("│");
	for(int i = 0; i < 1000000; i++) {
		if(rand() % 2 == 0) {
			printf("╱");
		} else {
			printf("╲");
		}

		if (((i + 1) % (w.ws_col - 1)) == 0) {
			printf("│");
			//fflush(stdout);
			//sleep(1);
		} 
	}
	return 0;
}

```
