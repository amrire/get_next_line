# get_next_line

`get_next_line` is a project written in C that provides a function to read a line from a file descriptor, one at a time. It is an essential utility often used in various programs to handle file reading efficiently. 

---

## Features

- Reads a single line, ending with a newline character, from a file descriptor.
- Handles multiple file descriptors simultaneously.
- Efficiently manages memory using a static buffer to avoid redundant memory allocations.
- Compatible with any file descriptor, such as files, standard input, or network sockets.

---

## Getting Started

### Prerequisites

- A C compiler (e.g., `gcc`) supporting the C99 standard or later.
- `make` (optional for building the project).

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/amrire/get_next_line.git
    cd get_next_line
    ```

2. Compile the program:
    ```bash
    make
    ```

### Usage

- Include the `get_next_line.h` header file in your project.
- Call the `get_next_line()` function by passing a valid file descriptor as an argument.

Example:
```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    char *line;

    if (fd < 0) {
        perror("Error opening file");
        return 1;
    }

    while ((line = get_next_line(fd)) != NULL) {
        printf("%s", line);
        free(line);
    }

    close(fd);
    return 0;
}
```

---

## Project Structure

- **`get_next_line.c`**: Contains the implementation of the `get_next_line()` function.
- **`get_next_line_utils.c`**: Contains utility functions used by `get_next_line`.
- **`get_next_line.h`**: Header file providing function declarations and necessary macros.
- **`Makefile`**: Build script for compiling the project.

---

## Configuration

You may customize the buffer size by defining the `BUFFER_SIZE` macro. The default buffer size is set in the Makefile or can be specified during compilation:

```bash
make BUFFER_SIZE=42
```

Or during manual compilation:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 -c get_next_line.c
```

---

## Testing

You can test the functionality of `get_next_line` by running the included test cases or creating your own test files.

1. Compile:
    ```bash
    make
    ```

2. Run your test program (e.g., `main.c`):
    ```bash
    ./a.out
    ```
