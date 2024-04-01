# NGINX RISC-V porting

### 1. NGINX configure
  1. move static linked crypt library
  - ``` mv TOOLCHAIN/sysroot/usr/lib/libcrypt.a TOOLCHAIN/sysroot/lib/libcrypt.a```
  2. RUN auto conf
  - ``` ./auto/configure --with-cc=`which riscv64-unknown-linux-gnu-gcc` --with-cpp=`which riscv64-unknown-linux-gnu-cpp` --without-http_rewrite_module --without-http_gzip_module --with-cc-opt="-static-libgcc -DAO_USE_PTHREAD_DEFS=1 -DNGX_HAVE_MAP_ANON=1 -DNGX_HAVE_LIBATOMIC=1 -DNGX_SYS_NERR=150 -Isrc/libatomic_ops" --with-libatomic --with-ld-opt="-static-libgcc -lpthread -lcrypt -static" ```
  3. move configures
   - ``` mv conf/* BUSYBOX/_install/conf ```

### 2. Make
  `make`
