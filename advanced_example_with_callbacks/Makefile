# manual/src/htmlman/intfc.html#s:c-advexample

SHELL:=bash

all:
# compile OCaml code to C object file (1); -custom is "custom runtime mode", which
# produces an output file that contains the runtime system and the bytecode; enables
# linking ocaml code with user-defined C functions; -output-obj produces a C obj file
	ocamlc -custom -output-obj -o modcaml.o mod.ml # modcaml.o mod.cmi mod.cmo

# compile stub code in modwrap.c (2)
	ocamlc -c modwrap.c # modwrap.o

# copy the bytecode runtime lib to mod.a, make writable; FIXME don't we already have the
# runtime from step (1)? "produces ... contains the runtime system..."?
	cp `ocamlc -where`/libcamlrun.a mod.a && chmod +w mod.a # mod.a

# add to mod.a the file produced at (1) and the compiled stub from (2)
	ar r mod.a modcaml.o modwrap.o # updates mod.a? yes, with modcaml.o modwrap.o

# NOTE none of the following could substitute for the cc command below; what is missing?
#	ocamlc -o prog main.c mod.a # doesn't seem to produce prog
#	ocamlc -o prog -I `ocamlc -where` main.c mod.a # doesn't seem to produce prog
#	ocamlc -custom -o prog -I `ocamlc -where` main.c mod.a # doesn't produce prog
#	ocamlc -custom -o prog main.c mod.a
#	ocamlopt -o prog mod.a main.c -cclib -lcurses
#	ocamlc -o prog -custom main.c mod.a # does'nt work

	cc -o prog main.c mod.a -lcurses -lpthread -lm -ldl # OK
#	cc -o prog -I `ocamlc -where` main.c mod.a -lcurses -lpthread -lm -ldl # OK
	./prog

clean:
	rm -f *.a *.o *.cmi *.cmo *.o prog
