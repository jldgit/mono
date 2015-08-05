##sgencounter

The SGen garbage collector was modified to count each time an object survives a collection. This was acheieved by adding a counter to the MonoObject struct and incrementing it inside of the GRAY_OBJECT_ENQUEUE macro as well as sgen_gray_object_enqueue function.

To access the data a new ICALL was made and it is accessed by a static class inside of mscorlib. This ICALL is located inside of the object.c file and is defined in object-internals.h. A new ICALL def was added to icall-def.h as per the instructions.

I chose to append the static class to the corlib/Mono/Runtime.cs file instead of creating a whole new folder and what not out of laziness.

You can see the branch differences here: [Compare Branches](https://github.com/mono/mono/compare/master...jldgit:sgencounter)

Here is output from this application with the modified SGen and mscorlib.

```
[mono] ~/mono/samples/sgencounter @ mono sgencounter.exe
Hello Mono World
Object age is 0.
Object age is 1.
Object age is 2.
Object age is 3.
Object age is 4.
Object age is 5.
Object age is 6.
Object age is 7.
Object age is 8.
Object age is 9.
Object age is 10.
Object age is 11.
Object age is 12.
Object age is 13.
Object age is 14.
Object age is 15.
Object age is 16.
Object age is 17.
Object age is 18.
Object age is 19.
Object age is 20.
Object age is 21.
Object age is 22.
Object age is 23.
Object age is 24.
Object age is 25.
Object age is 26.
Object age is 27.
Object age is 28.
Object age is 29.
Object age is 30.
Object age is 31.
Object age is 32.
Object age is 33.
Object age is 34.
Object age is 35.
Object age is 36.
Object age is 37.
Object age is 38.
Object age is 39.
Object age is 40.
Object age is 41.
Object age is 42.
Object age is 43.
Object age is 44.
Object age is 45.
Object age is 46.
Non null object
```
