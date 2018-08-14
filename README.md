# StaticMurmur

This repository provides a constexpr implementation of [MurmurHash3](https://github.com/aappleby/smhasher/blob/master/src/MurmurHash3.cpp) by Austin Appleby. Slight modifications have been made (such as removing `reinterpret_cast`s) in order to enable compile-time computation of hashes.

## Limitations

Only arrays of `char` are supported for the time being, and only the 32-bit version of MurmurHash3 has yet to be implemented. Other than that it should work as expected. Impact on compile-time is not known, but is should not be a problem. Tested on `g++` with `std=c++17` and `clang` with `std=c++1z`.

## Usage

Copy `StaticMurmur.hpp` and include it in your project, remember to compile with C++17. Usage is then pretty straight forward
```c++
#include "StaticMurmur.hpp"

int main(){
	// User has to provide a seed for the algorithm, in this case 123321u.
	constexpr hash = murmur::static_hash_x86_32("hellopleasework", 123321u);
	// the constant has been generated by Austion Appleby's version,
	// with the same string and hash.
	static_assert(hash == 3269627231);
	return hash;
}
```
g++ generates the following output (without opimization)
```asm
main:
	push	rbp
	mov	rbp, rsp
	mov	DWORD PTR -4[rbp], -1025340065
	mov	eax, -1025340065
	pop	rbp
	ret
```
If you have any suggestions or improvements, please feel free to help out.
