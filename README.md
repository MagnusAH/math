# OpenGL Math Library

Math library geared towards development with GLSL, for x86 only currently  
Library is compatable with GCC and Clang, not MSVC currently  
Library requires SSE support as a minimum, but AVX is recommended for the additional registers  

## Usage

### General

Library can be configure to either compile, inline, or force inline functions. If compiling is not desired `math.c` is unnecessary. `rodata.c` is a must have as it contains the identity values for 3x3 and 4x4 matrices. All files in `src` are required for the project and must be in the same directory. Function declarations are in `.h` files and implementations are in `.i` files. Function names in header files should be self explanitory as to the what the function does, standard parameter names are `o` for output, `a` for the first input, and `b` for the second input. 

### Vector

**Types**

`vec2f_t`  
2 element vector, with `float` as the element type  
1st element is accessable as `x`, `r` or `s`  
2nd element is accessable as `y`, `g` or `t`  
Vector as an array of floats is accessable as `f`  

`vec3f_t`  
3 element vector, with `float` as the element type  
1st element is accessable as `x`, `r` or `s`  
2nd element is accessable as `y`, `g` or `t`  
3rd element is accessable as `z`, `b` or `u`  
Vector as an array of floats is accessable as `f`  

`vec4f_t`  
4 element vector, with `float` as the element type  
1st element is accessable as `x`, `r` or `s`  
2nd element is accessable as `y`, `g` or `t`  
3rd element is accessable as `z`, `b` or `u`  
4th element is accessable as `w`, `a` or `v`  
Vector as an array of floats is accessable as `f`  

**Debugging**

Each vector type comes with two debugging macros, `VEC?F_FMT` and `VEC?F_ARG`, where `?` is representative of the number of elements in the vector.
They are used to print the value of the vector, eg: `printf(VEC4F_FMT, VEC4F_ARG(vec4f_t));`  

**Below is a list of functions where `?` is representative of the number of elements in the vector, being 2, 3 or 4**

Due to the vectors being a list of float, vectors are compatable with functions for smaller sizes, eg: 3 element vectors work with functions for 2 element vectors, only affecting the first two elements.  

`vec?f_addf(vec?f_t* o, vec?f_t* a, float b)`  
Adds `b` to each element of `a`, storing the result in `o`  
  
`vec?f_subf(vec?f_t* o, vec?f_t* a, float b)`  
Subtracts `b` from each element of `a`, storing the result in `o`  
  
`vec?f_mulf(vec?f_t* o, vec?f_t* a, float b)`  
Multiplies each element of `a` by `b`, storing the result in `o`  
  
`vec?f_divf(vec?f_t* o, vec?f_t* a, float b)`  
Divides each element of `a` by `b`, storing the result in `o`  
  
`vec?f_add(vec?f_t* o, vec?f_t* a, vec?f_t* b)`  
Adds vector `a` to vector `b`, storing the result in `o`  
  
`vec?f_sub(vec?f_t* o, vec?f_t* a, vec?f_t* b)`  
Subtracts vector `b` from vector `a`, storing the result in `o`  
  
`vec?f_mul(vec?f_t* o, vec?f_t* a, vec?f_t* b)`  
Multiplies vector `a` by vector `b`, storing the result in `o`  
  
`vec?f_div(vec4f_t* o, vec4f_t* a, vec4f_t* b)`  
Divides vector `a` by vector `b`, storing the result in `o`  
  
`vec?f_dot(float* o, vec?f_t* a, vec?f_t* b)`  
Calculates the dot product of vectors `a` and `b`, storing the result in `o`  
  
`void vec4f_cross(vec4f_t* restrict o, vec4f_t* a, vec4f_t* b)`  
Calculates the cross product of vectors `a` and `b`, storing the result in `o`  
Due to how the cross product is calculated, the output vector may not be any of the input vectors  

### Matrix

**Types**

`mat3f_t`  
3x3 matrix, with `float` as the element type  
Individual matrix elements are accessable as `m<row><column>`, eg: `m02` for the third element of the first row  
Matrix as an array of `vec3f_t` rows is accessable with `r`  
Matrix as an array of floats is accessable with `f`  
  
`mat4f_t`  
4x4 matrix, with `float` as the element type  
Individual matrix elements are accessable as `m<row><column>`, eg: `m02` for the third element of the first row  
Matrix as an array of `vec4f_t` rows is accessable with `r`  
Matrix as an array of floats is accessable with `f`  

**Debugging**

Each matrix type comes with two debugging macros, `MAT?F_FMT` and `MAT?F_ARG`, where `?` is representative of the size of the matrix.
They are used to print the value of the matrix, eg: `printf(MAT4F_FMT, MAT4F_ARG(mat4f_t));`  

**Below is a list of functions where `?` is representative of the size of the matrix, being 3 (3x3) or 4 (4x4)**
It is recommended to use 4x4 matrices in all cases due to them being significantly faster and that not all of the methods are currently implemented for 3x3 matrices. Unimplemented methods are marked as such in the header files.  

`mat?f_addf(mat?f_t* o, mat?f_t* a, float b)`  
Adds `b` to each elemet of `a`, storing the result in `o`  
  
`mat?f_subf(mat?f_t* o, mat?f_t* a, float b)`  
Subtracts `b` from each element of `a`, storing the result in `o`  
  
`mat?f_mulf(mat?f_t* o, mat?f_t* a, float b)`  
Multiplies each element of `a` by `b`, storing the result in `o`  
  
`mat?f_divf(mat?f_t* o, mat?f_t* a, float b)`  
Divides each element of `a` by `b`, sotring the result in `o`  
  
`mat?f_add(mat?f_t* o, mat?f_t* a, mat?f_t* b)`  
Adds matrix `a` to matrix `b`, storing the result in `o`  
  
`mat?f_sub(mat?f_t* o, mat?f_t* a, mat?f_t* b)`  
Subtracts matrix `b` from matrix `a`, storing the result in `o`  
  
`mat?f_mul(mat?f_t* o, mat?f_t* a, mat?f_t* b)`  
Multiples matrix `a` by matrix `b`, storing the result in `o`  
  
`mat?f_div(mat?f_t* o, mat?f_t* a, mat?f_t* b)`  
Divides matrix `a` by matrix `b`, storing the result in `o`  
  
`mat?f_iden(mat?f_t* o)`  
Sets matrix `o` to the identity matrix for the corresponding size  
  
`mat?f_inv(mat?f_t* o, mat?f_t* a)`  
Inverts matrix `a`, storing the result in `o`  
  
`mat?f_trans(mat?f_t* o, mat?f_t* a)`  
Transposes matrix `a`, sotring the result in `o`  
  
`mat?f_mulv?f(vec?f_t* o, mat?f_t* a, vec?f_t* b)`  
Multiples matrix `a`, by vector `b` (treated as a column vector), storing the result in vector `o`  

## SIMD compatable calculation of the inverse of a 4x4 matrix

// coming soon