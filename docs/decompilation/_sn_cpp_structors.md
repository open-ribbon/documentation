# _sn_cpp_structors()

Within main executables, there exists a method that initializes objects of classes, which is called a **constructor.** These constructors will be called for object creation. *Names for these are not yet finalized as some of them still read "UnkCtor"*
```
FontHack__Ctor
FileSys__Ctor
TmdLineObj__Ctor
Movie__Ctor
InputSys__Ctor
UnkCtor00
UnkCtor01
UnkCtor02
UnkCtor03
UnkCtor04
```
The procedure for getting all of these initialized is to make all the objects needed immediately or at least as soon as possible. The way that vib-ribbon takes care of this is to make an array `_CTOR_LIST__` with all of the above constructors. The `_sn_cpp_structors()` is then run inside `start()`.
```
void __fastcall _sn_cpp_structors(int sectionobj, int sectionobj_end)
{
  void (**ctor)(void);

  // Iterate through every entry in the _CTOR_LIST__ array.
  for ( ctor = (void (**)(void))sectionobj; (int)ctor < sectionobj_end; ++ctor )
  {
    // Run constructor inside its respective class. 
    if ( *ctor )
      (*ctor)();
  }
}
```
