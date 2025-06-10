from functools import lru_cache
from typing import List


def validate_positive_integer(n: int) -> None:
    """Ensure the input is a positive integer."""
    if not isinstance(n, int) or n <= 0:
        raise ValueError("Input must be a positive integer.")


def fibonacci_iterative(n: int) -> int:
    """Return the nth Fibonacci number (F(1) = 1, F(2) = 1) using iteration."""
    validate_positive_integer(n)
    a, b = 1, 1
    for _ in range(3, n + 1):
        a, b = b, a + b
    return a if n == 1 else b


@lru_cache(maxsize=None)
def fibonacci_recursive(n: int) -> int:
    """Return the nth Fibonacci number using memoized recursion."""
    validate_positive_integer(n)
    if n <= 2:
        return 1
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)


def fibonacci_sequence_1_to_n(n: int) -> List[int]:
    """
    Generate a list of Fibonacci numbers from F(1) to F(n).

    Args:
        n (int): Number of Fibonacci terms to generate.

    Returns:
        List[int]: Fibonacci sequence [F(1), F(2), ..., F(n)].
    """
    validate_positive_integer(n)
    if n == 1:
        return [1]
    sequence = [1, 1]
    for _ in range(3, n + 1):
        sequence.append(sequence[-1] + sequence[-2])
    return sequence


def main() -> None:
    n, nth = 10, 8

    print(f"Fibonacci numbers from F(1) to F({n}): {fibonacci_sequence_1_to_n(n)}")
    print(f"F({nth}) (iterative): {fibonacci_iterative(nth)}")
    print(f"F({nth}) (recursive): {fibonacci_recursive(nth)}")


if __name__ == "__main__":
    main()
