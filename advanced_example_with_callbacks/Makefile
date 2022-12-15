# manual/src/htmlman/intfc.html#s:c-advexample

SHELL:=bash

all:
	ocamlc -custom -output-obj -o modcaml.o mod.ml # modcaml.o mod.cmi mod.cmo
	ocamlc -c modwrap.c # modwrap.o
	cp `ocamlc -where`/libcamlrun.a mod.a && chmod +w mod.a # mod.a
	ar r mod.a modcaml.o modwrap.o # updates mod.a? yes, with modcaml.o modwrap.o
#	ocamlc -o prog main.c mod.a # doesn't seem to produce prog
#	ocamlc -o prog -I `ocamlc -where` main.c mod.a # doesn't seem to produce prog
	cc -o prog -I `ocamlc -where` main.c mod.a -lcurses -lpthread -lm -ldl
	./prog

clean:
	rm -f *.a *.o *.cmi *.cmo *.o
