
main: ../src/main.cpp Makefile
	g++ -o main ../src/main.cpp

main_static: ../src/main.cpp Makefile helper.a
	g++ -o main_static ../src/main.cpp helper.a

helper.a: helper.o
	ar -cvq helper.a helper.o

helper.o: ../src/helper.cpp
	g++ -Wall -fPIC -c ../src/helper.cpp 

libhelper.so: ../src/helper.cpp helper.o
	g++ -shared -Wl,-soname,libhelper.so.1.0.0 -o libhelper.so helper.o
	ln -sf libhelper.so libhelper.so.1.0.0

main_dynamic: ../src/main.cpp libhelper.so
	g++ -Wall -L. ../src/main.cpp -lhelper -o main_dynamic

clean:
	@rm -f main *.o *.a *.so main_* lib*

.PHONY: clean
