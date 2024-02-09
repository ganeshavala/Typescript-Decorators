# TypeScript Code Explanation

This repository contains two TypeScript files: `main.ts` and `PerfDecorators.ts`.

## main.ts

This file defines a class `Users` with two methods: `getUsers` and `getUser`. These methods are decorated with `@timing()`, which is a decorator function imported from `PerfDecorators`. The `getUser` method also has an `@important` decorator applied to its parameter.

The `Users` class itself is decorated with `@logTiming`.

Here's what each part does:

- `delay(time: number, data: T): Promise<T>`: This is a helper function that returns a promise that resolves with the provided data after a specified delay.

- `@logTiming`: This decorator logs the timings of all methods in the class that are decorated with `@timing()`.

- `@timing()`: This decorator measures the time it takes to execute the decorated method and logs it.

- `@important id: number`: The `@important` decorator marks the `id` parameter as important. This information is used by the `timing` decorator to log the values of important parameters.

- The `async` functions `getUsers` and `getUser` are methods of the `Users` class that simulate fetching users from a database or API. They use the `delay` function to simulate network latency.

- The IIFE (Immediately Invoked Function Expression) at the end creates an instance of `Users`, calls its methods, and then calls `printTimings` to log the timings.

## PerfDecorators.ts

This file defines the decorator functions `important`, `logTiming`, and `timing` that are used in the `main.ts` file.

Here's what each part does:

- `importantMetaDataKey`: This is a symbol used as a metadata key for the `important` decorator.

- `important(target, propertyKey, parameterIndex)`: This decorator function adds the index of the decorated parameter to the metadata of the method under the `importantMetaDataKey`.

- `logTiming(constructor)`: This decorator function extends the constructor of the decorated class to add a `__timings` property and a `printTimings` method. The `printTimings` method logs the contents of `__timings`.

- `timing()`: This decorator function modifies the descriptor of the decorated method to measure its execution time and log it. If the method has parameters decorated with `@important`, their values are also logged.
