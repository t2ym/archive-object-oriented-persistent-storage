# [Object-Oriented Persistent Storage for C++](https://t2ym.github.io/archive-object-oriented-persistent-storage/)

## Notes

- Archive of my senior thesis in 1998
- Platform: GNU C/C++ 2.7.2.1 on Linux 2.0.29 (32bit)
- Not working on current platforms

## Sample Code

```cpp
// Declarations
PersistentStorage *ps; // the persistent storage 
PersistentPointer pp;  // the persistent pointer
PersistentObject *obj; // the reference pointer

pp = ps->allocate(sizeof(PersistentObject)); // Allocate

  // Grab and Instantiate
  obj = new(pp.grab()) PersistentObject(parameters, ...); 
    obj->manipulate(parameters, ...); // Manipulate
  pp.release(); // Release 
  obj = 0; // Invalidate the reference pointer

  obj = pp.grabReadOnly(); // Read-only-Grab
    obj->reference(parameters, ...); // Reference
  pp.releaseReadOnly(); // Read-only-Release
  obj = 0; // Invalidate the reference pointer

  obj = pp.grab(); // Grab
  obj->~PersistentObject(); // Destruct

ps->destroy(pp); // Destroy (also Release)
ps->synchronize(); // Synchronize
```