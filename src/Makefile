CC=clang
LLD_PATH=/prog/rust/build/x86_64-unknown-linux-gnu/lld/bin

CFLAGS = --target=wasm32-wasmer-wasi \
         -O2 \
		 -include ../config.h \
		 --sysroot ../../wasix-libc/sysroot32 \
         -matomics \
         -mbulk-memory \
         -mmutable-globals \
         -pthread \
         -mthread-model posix \
         -ftls-model=local-exec \
         -fno-trapping-math \
		 -D_WASI_EMULATED_MMAN \
         -D_WASI_EMULATED_SIGNAL \
		 -D_WASI_EMULATED_PROCESS_CLOCKS \
         -Wall \
         -Wextra \
         -Werror \
         -Wno-null-pointer-arithmetic \
         -Wno-unused-parameter \
         -Wno-sign-compare \
         -Wno-unused-variable \
         -Wno-unused-function \
         -Wno-ignored-attributes \
         -Wno-missing-braces \
         -Wno-ignored-pragmas \
         -Wno-unused-but-set-variable \
         -Wno-unknown-warning-option \
         -Wno-parentheses \
         -Wno-shift-op-parentheses \
         -Wno-bitwise-op-parentheses \
         -Wno-logical-op-parentheses \
         -Wno-string-plus-int \
         -Wno-dangling-else \
         -Wno-unknown-pragmas \
         -MD \
         -MP

CLFLAGS = -Wl,--shared-memory \
          -Wl,--max-memory=4294967296 \
          -Wl,--import-memory \
          -Wl,--export-dynamic \
          -Wl,--export=__heap_base \
          -Wl,--export=__stack_pointer \
          -Wl,--export=__data_end \
          -Wl,--export=__wasm_init_tls \
          -Wl,--export=__tls_size \
          -Wl,--export=__tls_align \
          -Wl,--export=__tls_base

export PATH := $(LLD_PATH):$(PATH)

SRC = alias \
      arith_yacc \
      arith_yylex \
      builtins \
      cd \
      error \
      eval \
      exec \
      expand \
      histedit \
      init \
      input \
      jobs \
      mail \
      main \
      memalloc \
      miscbltin \
      mystring \
      nodes \
      output \
	  options \
      parser \
      redir \
      show \
      signames \
      syntax \
      system \
      trap \
      var \
	  times \
	  test \
	  printf

OBJS = $(SRC:=.o)

all: dash

dash: $(SRC)
	clang $(CFLAGS) $(CLFLAGS) \
              $(OBJS) \
              -o $@.wasm

mkinit: $(SRC)
	clang $(CFLAGS) $(CLFLAGS) \
	          $@.c \
              $(OBJS) \
              -o $@.wasm

mknodes: $(SRC)
	clang $(CFLAGS) $(CLFLAGS) \
	          $@.c \
              $(OBJS) \
              -o $@.wasm

mksignames: $(SRC)
	clang $(CFLAGS) $(CLFLAGS) \
	          $@.c \
              $(OBJS) \
              -o $@.wasm

mksyntax: $(SRC)
	clang $(CFLAGS) $(CLFLAGS) \
	          $@.c \
              $(OBJS) \
              -o $@.wasm      

%: %.c
	clang $(CFLAGS) \
              $@.c \
			  -c \
              -o $@.o

clean:
	rm -f *.o
	rm -f *.s
	rm -f *.ll
	rm -f *~
	rm -f *.wasm
