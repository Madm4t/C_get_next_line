# get_next_line

[![License](https://img.shields.io/badge/license-Unlicense-blue)](/LICENSE)

A robust, Norm-compliant C implementation of the `get_next_line()` function, reading and returning the next line from any file descriptor with efficient buffering and support for multiple descriptors.

## Table of Contents

- [About](#about)  
- [Features](#features)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Example](#example)  

## About

`get_next_line` reads from a file descriptor one line at a time (including the trailing newline `\n`) and returns it as a heap-allocated string. It handles internal buffering, dynamic memory management, and preserves the remainder between calls—ideal for parsing text files, user input, or any stream data.
`get_next_line_bonus` supports reading from multiple file descriptors at the same time.

This project was built for the 42 School curriculum under strict Norm guidelines to deepen your understanding of I/O, pointers, and dynamic allocation in C.

## Features

- **Line-by-line reading**: Returns each line on successive calls, including the newline character.  
- **Multiple descriptors**: Maintains independent buffers for different file descriptors.  
- **Configurable buffer**: Uses a compile-time `BUFFER_SIZE` macro.  
- **Norm-compliant**:  
  - No forbidden standard functions (only `read`, `malloc`, `free`).  
  - 25 lines max per function.  
  - 80-column width limit.  
  - 4 functions per file.  
  - Max 4 parameters per function.  

## Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/Madm4t/C_get_next_line.git
   cd C_get_next_line

## Usage

1. Include the header in your source file:
   ```bash
   #include "get_next_line.h"
2. Compile you program together with the get_next_line.c and get_next_line_utils.c files e.g.:
   ```bash
   gcc -Wall -Wextra -Werror main.c get_next_line.c and get_next_line_utils.c -o my_app

3. If you want to read from multiple file descriptors use the _bonus extension:
   ```bash
   #include "get_next_line_bonus.h"
   gcc -Wall -Wextra -Werror main.c get_next_line_bonus.c and get_next_line_utils_bonus.c -o my_app
   gcc -Wall -Wextra -Werror main.c get_next_line_bonus.c and get_next_line_utils_bonus.c -o my_app

## Example
***main.cpp*** using get_next_line
```c
int	main(void)
{
	int		fd;
	char	*line;

	fd = open("test.txt", O_RDONLY);
	while ((line = get_next_line(fd)))
	{
		printf("-->%s", line);
		free(line);
	}
	close(fd);
	return(0);
}
```
***main.cpp*** using get_next_line_bonus
```c
int main(void)
{
	int		fd1;
	int		fd2;
	int		fd3;
	int		count;
	char	*line;

	count = 1;
	fd1 = open("test1.txt", O_RDONLY);
	fd2 = open("test2.txt", O_RDONLY);
	fd3 = open("test3.txt", O_RDONLY);

	while(count < 7)
	{
		line = get_next_line(fd1);
		printf("%d -> %s", count, line);
		free(line);

		line = get_next_line(fd2);
		printf("%d -> %s", count, line);
		free(line);

		line = get_next_line(fd3);
		printf("%d -> %s", count, line);
		free(line);
		count++;
	}
	close(fd1);
	close(fd2);
	close(fd3);
	return (0);
}
```
