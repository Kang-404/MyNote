# Compound Types
A compound type is a type that is defined in terms of another type.
## References
A reference defines an alternative name for an object.  
**_Note_** : A reference is not an object.Instead, a reference is just *another name* for an already existing object.   

___Reference Definitions:___
``` C++
int i = 1024, i2 = 2048;    // i and i2 are both ints
int &r = i, r2 = i2;        // r is reference bound to i; r2 is an int
int i3 = 1024, &ri = i3;    // i3 is an int;ri is a reference bound to i3
int &r3 = i3, &r4 = i2;     // both r3 and r4 are references
```   


The *type* of a reference and the objet to which the reference refers must match exactly.  
A reference must be bound only to an object, not to a literal or to the result of a more general expression.
``` C++
int &refVal4 = 10;      // error: initializer must be an object
double dval = 3.14; 
int &refVal5 = dval;    // error: initializer must be an int object
```

## Pointers
*Same*:  
- A pointer is a compound type that "points" to another type.
- Pointers are used for indirect access to other objects.  

*Different*:  
- A pointer is an *object* in its own right. 
- A pointer can point to several *different objects*.    
- A pointer need *not be initialized* at the times it is defined.

**_Note_** : We may dereference only a vaild pointer that points an object.

**_Null Pointer_** :  
A null pointer does not point to any object.
``` C++
int *p1 = nullptr;      // equivalent to *p1 = 0;
int *p2 = 0;            // directly initializes p2 from the literal constant 0
// must #include cstdlib
int *p3 = NULL;
```

___void* Pointers___:  
The type of the object at that address is unknown.  
We use a __void*__ pointer to deal with memory as memory, rather than using the pointer to access the object stored in that memory.

## Compound Type Declarations
``` C++
int ival = 1024;
int *pi = &ival;
int **ppi = &pi;
int *&r = pi;       // r is a reference to the pointer p
```
The easiest way to understand the type of *r* is to read the definition right to left.    
The symbol closest to the name of the variable is the one that has the most immediate effect on the variable's type.   
***Tip***: It can be easier to understand complicated pointer or reference declarations if you read them from right to left.
