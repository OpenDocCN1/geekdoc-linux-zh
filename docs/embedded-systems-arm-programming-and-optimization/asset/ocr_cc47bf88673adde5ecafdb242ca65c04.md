# 242 APPENDIX B NEON Intrinsic Reference

+   - Set as an array:
int8x8_t a;
for (i=0;i<8;i++) a[i]=i*2;

+   - Read as an array:
for (i=0;i<8;i++) printf("%d",a[i]);
printf("\n");

As shown below, NEON intrinsics have a suffix that specifies the type and size of their elements. Note the conspicuous lack of 64-bit floating point.

+   - _s8 signed 8-bit integer
- _u8 unsigned 8-bit integer
- _s16 signed 16-bit integer
- _u16 unsigned 16-bit integer
- _s32 signed 32-bit integer
- _u32 unsigned 32-bit integer
- _p8 8-bit polynomial
- _p16 16-bit polynomial
- _f16 16-bit float
- _f32 32-bit float

Normal, double-word intrinsics assume a 64-bit total width, so the vector size is implied by the element size. For example, the _s8 intrinsic operate on a 64/8=8-element vector. As described above, the "q" specifies a 128-bit vector, so an intrinsic ending with q_s8 would operate on a 128/16=16-element vector.

Some intrinsics are used to instance a vector. For example, the vcreate intrinsics map each 8-bit field from a scalar to the elements of an 8-element vector:

```
// set vector from least significant byte,
// i.e. a[0]=55, a[7]=5514
a = vcreate_s8(0x0D0C0C0A0806040200);
```

The vdup intrinsic sets each element to a specified scalat value:

```
int8x16_t b;
a = vdup_n_s8(5); // set all 8 elements to 5
b = vdup_n_s8(5); // set all 16 elements to 5
```