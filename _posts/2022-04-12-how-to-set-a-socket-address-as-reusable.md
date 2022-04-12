---
excerpt_separator: <!--end_excerpt-->
---

Did you just get an "address already in use" error while calling bind()?

Use the following snippet to get rid of it:

```C
int enable = 1;
if (setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &enable, sizeof(int)) < 0)
    perror("setsockopt(SO_REUSEADDR) failed");
```
<!--end_excerpt-->
