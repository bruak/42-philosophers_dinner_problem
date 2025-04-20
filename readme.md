# Philosophers Dining Problem

A multithreaded solution to the classic Dining Philosophers problem, implementing thread synchronization using mutexes in C.

## Table of Contents
- [Philosophers Dining Problem](#philosophers-dining-problem)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Problem Description](#problem-description)
  - [Features](#features)
  - [Technical Implementation](#technical-implementation)
    - [Core Components](#core-components)
    - [Data Structures](#data-structures)
  - [Usage](#usage)
    - [Parameters](#parameters)
    - [Example](#example)
  - [Project Structure](#project-structure)
  - [Requirements](#requirements)
  - [Compilation](#compilation)
    - [Additional Make Commands](#additional-make-commands)

## Overview

The Dining Philosophers problem is a classic synchronization and concurrency problem in computer science. This project implements a solution using POSIX threads and mutexes to handle resource sharing and prevent deadlocks and race conditions.

## Problem Description

- N philosophers sit at a round table with N forks
- Each philosopher needs two forks to eat (one from their left and one from their right)
- Philosophers alternate between three states: eating, thinking, or sleeping
- When a philosopher finishes eating, they put down their forks and start sleeping
- Once done sleeping, they start thinking
- The simulation stops when a philosopher dies of starvation or when all philosophers have eaten a specified number of times

## Features

- Precise time management with microsecond accuracy
- Deadlock prevention mechanisms
- Thread-safe operations using mutexes
- Clear status messages for each philosopher's actions
- Death detection when a philosopher hasn't eaten within the time limit
- Optional meal counter to stop the simulation after all philosophers have eaten enough

## Technical Implementation

### Core Components

- **Threads**: Each philosopher is represented by a thread
- **Mutexes**: Used to protect shared resources (forks) and prevent race conditions
- **Time Management**: Ensures accurate timing for eating, sleeping, and detecting starvation
- **Synchronization**: Coordinates actions between philosophers to avoid deadlocks

### Data Structures

- `t_philo`: Contains information about each philosopher including ID, fork assignments, and meal counts
- `t_data`: Stores simulation parameters and shared resources like mutexes and flags

## Usage

```bash
./philo [number_of_philosophers] [time_to_die] [time_to_eat] [time_to_sleep] [optional: number_of_times_each_philosopher_must_eat]
```

### Parameters

- `number_of_philosophers`: Number of philosophers and forks (1-200)
- `time_to_die`: Time in milliseconds after which a philosopher dies if they haven't started eating (must be > 60ms)
- `time_to_eat`: Time in milliseconds that a philosopher takes to eat (must be > 60ms)
- `time_to_sleep`: Time in milliseconds that a philosopher spends sleeping (must be > 60ms)
- `number_of_times_each_philosopher_must_eat` (optional): If specified, simulation stops when all philosophers have eaten at least this many times

### Example

```bash
./philo 5 800 200 200 7
```

This will create a simulation with 5 philosophers where:
- Philosophers die if they don't eat within 800ms
- Each philosopher takes 200ms to eat
- Each philosopher sleeps for 200ms after eating
- The simulation ends when all philosophers have eaten at least 7 times

## Project Structure

- `main.c`: Entry point and program initialization
- `init.c`: Initialization of data structures and mutexes
- `start.c` & `start_2.c`: Core simulation logic and philosopher routines
- `allocation.c`: Dynamic memory allocation
- `free_destroy.c` & `free_destroy_2.c`: Resource cleanup
- `one_philo.c`: Special handling for edge case with single philosopher
- `time_sleep.c`: Time management functions
- `first_arg_check.c`: Command line argument parsing and validation
- `philo.h`: Header file with function prototypes and data structures

## Requirements

- Unix-based operating system (Linux/macOS)
- C compiler (GCC recommended)
- pthread library
- make

## Compilation

```bash
make
```

This will compile the project and create the `philo` executable.

### Additional Make Commands

- `make clean`: Remove object files
- `make fclean`: Remove object files and executable
- `make re`: Recompile from scratch