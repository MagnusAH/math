# OpenGL Math Library

Math library geared towards development with GLSL and C, for x86 only currently  
Library is compatable with GCC and Clang, not MSVC at the moment  
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

The inverse of a matrix can be calculated in multiple ways, however the classical adjoint method works the best for SIMD as it has the same calculation applied to multiple elements. Using this method the the inverse is found by calculating the matrix of cofactors, dividing each element by the determinant of the matrix, multiplying by an alternating sign grid, and then transposing the matrix.

The matrix of cofactors for the 4x4 matrix *m* with resultant matrix *o* can be written as the following, in the format of *m<row><column>*.

> o00 = m11 * (m22 * m33 - m23 * m32) - m12 * (m21 * m33 - m23 * m31) + m13 * (m21 * m32 - m22 * m31)  
> o01 = m10 * (m22 * m33 - m23 * m32) - m12 * (m20 * m33 - m23 * m30) + m13 * (m20 * m32 - m22 * m30)  
> o02 = m10 * (m21 * m33 - m23 * m31) - m11 * (m20 * m33 - m23 * m30) + m13 * (m20 * m31 - m21 * m30)  
> o03 = m10 * (m21 * m32 - m22 * m31) - m11 * (m20 * m32 - m22 * m30) + m12 * (m20 * m31 - m21 * m30)  
>   
> o10 = m01 * (m22 * m33 - m23 * m32) - m02 * (m21 * m33 - m23 * m31) + m03 * (m21 * m32 - m22 * m31)  
> o11 = m00 * (m22 * m33 - m23 * m32) - m02 * (m20 * m33 - m23 * m30) + m03 * (m20 * m32 - m22 * m30)  
> o12 = m00 * (m21 * m33 - m23 * m31) - m01 * (m20 * m33 - m23 * m30) + m03 * (m20 * m31 - m21 * m30)  
> o13 = m00 * (m21 * m32 - m22 * m31) - m01 * (m20 * m32 - m22 * m30) + m02 * (m20 * m31 - m21 * m30)  
>   
> o20 = m01 * (m12 * m33 - m13 * m32) - m02 * (m11 * m33 - m13 * m31) + m03 * (m11 * m32 - m12 * m31)  
> o21 = m00 * (m12 * m33 - m13 * m32) - m02 * (m10 * m33 - m13 * m30) + m03 * (m10 * m32 - m12 * m30)  
> o22 = m00 * (m11 * m33 - m13 * m31) - m01 * (m10 * m33 - m13 * m30) + m03 * (m10 * m31 - m11 * m30)  
> o23 = m00 * (m11 * m32 - m12 * m31) - m01 * (m10 * m32 - m12 * m30) + m02 * (m10 * m31 - m11 * m30)  
>   
> o30 = m01 * (m12 * m23 - m13 * m22) - m02 * (m11 * m23 - m13 * m21) + m03 * (m11 * m22 - m12 * m21)  
> o31 = m00 * (m12 * m23 - m13 * m22) - m02 * (m10 * m23 - m13 * m20) + m03 * (m10 * m22 - m12 * m20)  
> o32 = m00 * (m11 * m23 - m13 * m21) - m01 * (m10 * m23 - m13 * m20) + m03 * (m10 * m21 - m11 * m20)  
> o33 = m00 * (m11 * m22 - m12 * m21) - m01 * (m10 * m22 - m12 * m20) + m02 * (m10 * m21 - m11 * m20)  

This however can be simplefied using the following 4 element groups. 

> i01 = m01, m00, m00, m00  
> i02 = m02, m02, m01, m01  
> i03 = m03, m03, m03, m02  
>   
> i11 = m11, m10, m10, m10  
> i12 = m12, m12, m11, m11  
> i13 = m13, m13, m13, m12  
>   
> i21 = m21, m20, m20, m20  
> i22 = m22, m22, m21, m21  
> i23 = m23, m23, m23, m22  
>   
> i31 = m31, m30, m30, m30  
> i32 = m32, m32, m31, m31  
> i33 = m33, m33, m33, m32  

Substituting these in we get a new formula, where each calculation is on a 4 element vector, perfect for SIMD and taking it from 244 to 56 mathematical operations.

> o0 = i11 * (i22 * i33 - i23 * i32) - i12 * (i21 * i33 - i23 * i31) + i13 * (i21 * i32 - i22 * i31)  
> o1 = i01 * (i22 * i33 - i23 * i32) - i02 * (i21 * i33 - i23 * i31) + i03 * (i21 * i32 - i22 * i31)  
> o2 = i01 * (i12 * i33 - i13 * i32) - i02 * (i11 * i33 - i13 * i31) + i03 * (i11 * i32 - i12 * i31)  
> o3 = i01 * (i12 * i23 - i13 * i22) - i02 * (i11 * i23 - i13 * i21) + i03 * (i11 * i22 - i12 * i21)  

However, there is more substitution that can be done if we rewrite the formula as the following.

> o0 = i11 * (i22 * i33 - i23 * i32) + i12 * (i23 * i31 - i21 * i33) + i13 * (i21 * i32 - i22 * i31)  
> o1 = i01 * (i22 * i33 - i23 * i32) + i02 * (i23 * i31 - i21 * i33) + i03 * (i21 * i32 - i22 * i31)  
> o2 = i31 * (i02 * i13 - i03 * i12) + i32 * (i03 * i11 - i01 * i13) + i33 * (i01 * i12 - i02 * i11)  
> o3 = i21 * (i02 * i13 - i03 * i12) + i22 * (i03 * i11 - i01 * i13) + i23 * (i01 * i12 - i02 * i11)  

This allows us to simplify using the following intermediary groups.

> d0 = i22 * i33 - i23 * i32  
> d1 = i23 * i31 - i21 * i33  
> d2 = i21 * i32 - i22 * i31  
> d3 = i02 * i13 - i03 * i12  
> d4 = i03 * i11 - i01 * i13  
> d5 = i01 * i12 - i02 * i11  

Substituting these in we get a new formula, taking us from 56 to 38 mathematical operations.

> o0 = i11 * d0 + i12 * d1 + i13 * d2  
> o1 = i01 * d0 + i02 * d1 + i03 * d2  
> o2 = i31 * d3 + i32 * d4 + i33 * d5  
> o3 = i21 * d3 + i22 * d4 + i23 * d5  

The determinant of the matrix can then be calculated using the first row of the matrix of mirrors and the first row of the original matrix.

> determinant = m00 * o00 - m01 * m02 + m02 * o02 - m03 * o03

From here there is not much to do in terms of mathematical optimization, just programmatical optimization. Example C code for inverting a 4x4 matrix of floats can be seen below using SSE intrinsics.

```
/*
Method uses
 - 20 permutations
 - 8 shuffles
 - 8 subtractions
 - 9 additions
 - 29 multiplications
 - 1 reciprical
*/
void inverse(float* matrix)
{
	// load input matrix
	__m128
		r0 = _mm_load_ps(matrix),
		r1 = _mm_load_ps(matrix + 4),
		r2 = _mm_load_ps(matrix + 8),
		r3 = _mm_load_ps(matrix + 12);
		
	// permute into 4 element groups
	__m128
		i01 = _mm_permute_ps(r0, 0b00000001), 
		i02 = _mm_permute_ps(r0, 0b01011010), 
		i03 = _mm_permute_ps(r0, 0b10111111),
		
		i11 = _mm_permute_ps(r1, 0b00000001), 
		i12 = _mm_permute_ps(r1, 0b01011010), 
		i13 = _mm_permute_ps(r1, 0b10111111),
		
		i21 = _mm_permute_ps(r2, 0b00000001), 
		i22 = _mm_permute_ps(r2, 0b01011010), 
		i23 = _mm_permute_ps(r2, 0b10111111),
		
		i31 = _mm_permute_ps(r3, 0b00000001),
		i32 = _mm_permute_ps(r3, 0b01011010), 
		i33 = _mm_permute_ps(r3, 0b10111111);
		
	// compute intermediary groups
	__m128
		j0 = _mm_sub_ps(_mm_mul_ps(i22, i33), _mm_mul_ps(i23, i32)), // i22 * i33 - i23 * i32
		j1 = _mm_sub_ps(_mm_mul_ps(i23, i31), _mm_mul_ps(i21, i33)), // i23 * i31 - i21 * i33
		j2 = _mm_sub_ps(_mm_mul_ps(i21, i32), _mm_mul_ps(i22, i31)), // i21 * i32 - i22 * i31
		j3 = _mm_sub_ps(_mm_mul_ps(i02, i13), _mm_mul_ps(i03, i12)), // i02 * i13 - i03 * i12
		j4 = _mm_sub_ps(_mm_mul_ps(i03, i11), _mm_mul_ps(i01, i13)), // i03 * i11 - i01 * i13
		j5 = _mm_sub_ps(_mm_mul_ps(i01, i12), _mm_mul_ps(i02, i11)); // i01 * i12 - i02 * i11
		
	// compute matrix of minors
	__m128
		// i11 * d0 + i12 * d1 + i13 * d2
		m0 = _mm_add_ps(_mm_add_ps(_mm_mul_ps(i11 , j0), _mm_mul_ps(i12 , j1)), _mm_mul_ps(i13 , j2)), 
		// i01 * d0 + i02 * d1 + i03 * d2
		m1 = _mm_add_ps(_mm_add_ps(_mm_mul_ps(i01 , j0), _mm_mul_ps(i02 , j1)), _mm_mul_ps(i03 , j2)), 
		// i31 * d3 + i32 * d4 + i33 * d5
		m2 = _mm_add_ps(_mm_add_ps(_mm_mul_ps(i31 , j3), _mm_mul_ps(i32 , j4)), _mm_mul_ps(i33 , j5)), 
		// i21 * d3 + i22 * d4 + i23 * d5
		m3 = _mm_add_ps(_mm_add_ps(_mm_mul_ps(i21 , j3), _mm_mul_ps(i22 , j4)), _mm_mul_ps(i23 , j5));
		
	// determinant intermediary, determinant is [0] - [1] + [2] - [3] of r0 * m0
	// using this saves us 3 multiplications
	__m128
		di = _mm_mul_ps(r0, m0);
		
	// calculate alternating sign inverse determinant for rows 0 and 2
	// multiplication is significantly faster than division so we multiply by the invserse determinant instead of dividing
	__m128
		asid0 = _mm_rcp_ps(
					_mm_add_ps(
						_mm_sub_ps(_mm_permute_ps(di, 0b01000100), _mm_permute_ps(di, 0b00010001)), 
						_mm_sub_ps(_mm_permute_ps(di, 0b11101110), _mm_permute_ps(di, 0b10111011))
						)
					);

	// calculate alternating sign inverse determinant for rows 1 and 3
	__m128
		asid1 = _mm_permute_ps(asid0, 0b00010001);
		
	// calculate matrix of cofactors
	m0 = _mm_mul_ps(m0, asid0);
	m1 = _mm_mul_ps(m1, asid1);
	m2 = _mm_mul_ps(m2, asid0);
	m3 = _mm_mul_ps(m3, asid1);

	// compute transpose intermediary group
	__m128
		// [0], [1] of m0 and m1 => {m0[0], m1[0], m0[1], m1[1]}
		tr01a = _mm_permute_ps(_mm_shuffle_ps(m0, m1, 0b01000100), 0b11011000), 
		// [2], [3] of m0 and m1 => {m0[2], m1[2], m0[3], m1[3]}
		tr01b = _mm_permute_ps(_mm_shuffle_ps(m0, m1, 0b11101110), 0b11011000), 
		// [0], [1] of m2 and m3 => {m2[0], m3[0], m2[1], m3[1]}
		tr23a = _mm_permute_ps(_mm_shuffle_ps(m2, m3, 0b01000100), 0b11011000), 
		// [2], [3] of m2 and m3 => {m2[2], m3[2], m2[3], m3[3]}
		tr23b = _mm_permute_ps(_mm_shuffle_ps(m2, m3, 0b11101110), 0b11011000); 
	
	// transpose matrix
	__m128
		o0 = _mm_shuffle_ps(tr01a, tr23a, 0b01000100), // m0[0], m1[0], m2[0], m3[0]
		o1 = _mm_shuffle_ps(tr01a, tr23a, 0b11101110), // m0[1], m1[1], m2[1], m3[1]
		o2 = _mm_shuffle_ps(tr01b, tr23b, 0b01000100), // m0[2], m1[2], m2[2], m3[2]
		o3 = _mm_shuffle_ps(tr01b, tr23b, 0b11101110); // m0[3], m1[3], m2[3], m3[3]
		
	// store result
	_mm_store_ps(matrix, o0);
	_mm_store_ps(matrix + 4, o1);
	_mm_store_ps(matrix + 8, o2);
	_mm_store_ps(matrix + 12, o3);
}
```