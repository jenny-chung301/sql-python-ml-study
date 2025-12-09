# Week 5 - Deep-ML Problems

## Table of Contents

-   [1 - Matrix-Vector Dot Product](#question-1)
-   [2 - Transpose of a Matrix](#question-2)
-   [83 - Dot Product Calculator](#question-3)
-   [5 - Scalar Multiplication of a Matrix](#question-4)
-   [76 - Calculate Cosine Similarity Between Vectors](#question-5)

------------------------------------------------------------------------

<a id="question-1"></a>
## 1 - Matrix-Vector Dot Product

**Solution:**

``` python
def matrix_dot_vector(a: list[list[int|float]], b: list[int|float]) -> list[int|float]:
	# Return a list where each element is the dot product of a row of 'a' with 'b'.
	# If the number of columns in 'a' does not match the length of 'b', return -1.
	if len(a[0]) != len(b):
		return -1
	
	result = []
	for row in a:
		result.append(sum(j*k for j,k in zip(row, b)))

	return result
```

------------------------------------------------------------------------

<a id="question-2"></a>
## 2 - Transpose of a Matrix

**Solution:**

``` python
def transpose_matrix(a: list[list[int|float]]) -> list[list[int|float]]:
	b = [list(row) for row in list(zip(*a))]
	return b
```

------------------------------------------------------------------------

<a id="question-3"></a>
## 83 - Dot Product Calculator

**Solution:**

``` python
import numpy as np

def calculate_dot_product(vec1, vec2) -> float:
	"""
	Calculate the dot product of two vectors.
	Args:
		vec1 (numpy.ndarray): 1D array representing the first vector.
		vec2 (numpy.ndarray): 1D array representing the second vector.
	"""
	# Your code here
	return np.dot(vec1, vec2)
```

------------------------------------------------------------------------

<a id="question-4"></a>
## 5 - Scalar Multiplication of a Matrix

**Solution:**

``` python
def scalar_multiply(matrix: list[list[int|float]], scalar: int|float) -> list[list[int|float]]:

	result = [[el*scalar for el in row] for row in matrix]
	return result
```

------------------------------------------------------------------------

<a id="question-5"></a>
## 76 - Calculate Cosine Similarity Between Vectors

**Solution:**

``` python
import numpy as np

def cosine_similarity(v1, v2):
	# Implement your code here
	return np.round((v1*v2).sum() / np.sqrt(((v1**2).sum()*(v2**2).sum())),3)

```

------------------------------------------------------------------------
