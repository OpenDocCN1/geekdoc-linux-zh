![](bbox=[0.055, 0.135, 0.525, 0.405])

Figure 13.1: LSB Development Environment

+   - Use the LSB-compliant libraries. Using the Development Environment stub libraries has the advantage that link errors will occur if you attempt to use non-LSB interfaces.
+   - Ensure that the binary uses the LSB dynamic linker instead of the standard Linux linker for that architecture. For example, on x86 machines /lib/ld-lsb.so.1 should be used instead of /lib/ld-linux.so.2.

If you use `lsb-build-chroot`, then the first two changes are taken care of automatically. The way to achieve the third one will be compiler-dependent; as an example, with gcc this is done by editing the `specs` configuration file.

# 13.7.2 Integration with an IDE

Integration of `lsb-build-cc` with an IDE should be fairly straightforward, as the only change required is to call **lsbcc** instead of the normal compiler. In the case of `lsb-build-chroot` it would be necessary to run the compilation process inside of the `chroot`. This could be achieved using a helper program, or perhaps communicating with a compilation daemon that is running inside the `chroot`.