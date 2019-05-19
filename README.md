#ifndef "Stack_Libro.h"
#define "Stack_Libro.h"
#include <iostream>
#include <stdlib.h>
#include <stdio.h>

class Libro;
class Stack_lib;

#endif
#define STACK_DE_LIBROS_H
#include "Libro.h"

 class Stack_lib{
            private:
                    Libro book[5];

            public:
                    Stack_lib();
                    Stack_lib(Libro _book[5]);
                    void push(Libro);
                    Libro pop();
                    bool _empty();
};


#endif // STACK_DE_LIBROS_H
#ifndef STACK_LLS_H
#define STACK_LLS_H


class Stack_lls{
	struct Nodo{
    		Libro lib;
   	        Nodo *link;
	};

        private:
                Nodo *punt_lib;

        public:
                Stack_lls();
                void push(Libro);
                Libro pop();
                bool _empty();

};


#endif // STACK_LLS_H
#ifndef LIBRO_H
#define LIBRO_H
#include <stdlib.h>
#include <stdio.h>
#include <iostream>

class Libro {
        private : string titulo;
                  string autor;
                  int cant_de_pag;

        public : Libro();
             	 Libro(const Libro&);
             	 Libro(string, string , int);
		         void setTitulo(string);
             	 void setAutor(string);
     		     void setCant_de_pag(int);
             	 string getTitulo();
             	 string getAutor();
             	 int getCant_de_pag();

};

#endif // LIBRO_H



#include "Stack_Libro.h"

using namespace std;



class Libro {
	private : string titulo;
	          string autor;
	          int cant_de_pag;

        public : Libro();
             	 Libro(const Libro&);
             	 Libro(string, string , int);
		         void setTitulo(string);
             	 void setAutor(string);
     		     void setCant_de_pag(int);
             	 string getTitulo();
             	 string getAutor();
             	 int getCant_de_pag();

};

Libro :: Libro(){
	this-> titulo = '';
	this-> autor = '';
	this-> cant_de_pag = 0;
}

Libro :: Libro(const Libro &nuevo){
	this-> titulo = nuevo.titulo;
	this-> autor = nuevo.autor;
	this-> cant_de_pag = nuevo.cant_de_pag;
}

Libro :: Libro (string _titulo , string _autor , int _cant_de_pag){
	this-> titulo = _titulo;
	this-> autor = _autor;
	this-> cant_de_pag = _cant_de_pag;
}

void Libro :: setTitulo (string _titulo){
	this-> titulo = _titulo;
}

void Libro :: setAutor (string _autor){
	this-> autor = _autor;
}

void Libro :: setCant_de_pag(int _cant_de_pag){
	this-> cant_de_pag = _cant_de_pag;
}

string Libro :: getTitulo (){
	return this -> titulo;
}

string Libro :: getAutor (){
	return this -> autor;
}

int Libro :: getCant_de_pag(){
	return this -> cant_de_pag;
}



#include "Stack_Libro.h"

//El ultimo libro ingresado se guarda en la ultima posicion del arreglo

typedef Libro vacio("","",0);

 class Stack_lib{
            private:
                    Libro book[5];

            public:
                    Stack_lib();
                    //Stack_lib(Libro);
                    //Stack_lib(const Libro&);
                    void push(Libro);
                    Libro pop();
                    bool _empty();
};

Stack_lib :: Stack_lib(){
    int i;
    for(i=0;i<5;i++){
        book[i]=vacio;
    }
}

void Stack_lib :: push(Libro _lib){
    int i;
    for(i=0;i<5;i++){
        if(book[i] == vacio){
            book[i]=_lib;
            exit(-1);
        }
    }
}

Libro Stack_lib :: pop(){
    int i;
    Libro aux;
    for(i=0;i<5;i++){
        if((book[i+1] == vacio) || (i == 4)){ //se ve si la posicion del arreglo actual es la ultima, es decir, si el que sigue esta vacio o si esta en la ultima posicion del arreglo (posicion 99)
            aux=book[i];
            book[i]=vacio;
        }
    }
    return aux;
}

bool Stack_lib :: _empty(){ // return TRUE si el arreglo esta vacio, return FALSE si el arreglo tiene elementos
    return (book[0] == vacio);
}



#include "Stack_de_libros.h"
#include "Stack_lls.h"

using namespace std;


void OrdenarMisLecturas(Stack_lib lib);

int main()
{
    Stack_lib _libro;
    Libro aux;
    Libro vacio("","",0);
    string _titulo, _autor;
    int i,paginas;
    cout <<"Ingrese Titulo, Autor y Cantidad de paginas de cinco libros:"<<endl;
    for(i=0;i<5;i++){
        cout <<"Titulo: "<<endl;
        cin >> _titulo;
        cout <<"Autor/a: "<<endl;
        cin >> _autor;
        cout <<"Cantidad de paginas: "<<endl;
        cin >> paginas;
        aux(_titulo,_autor,paginas);
        _libro.push(aux);
        _titulo = "";
        _autor = "";
        paginas = 0;
        aux = vacio; //vacio---> Libro vacio (hay que definirlo)
        system("clear");
    }

    OrdenarMisLecturas(_libro);
    return 0;
}

void OrdenarMisLecturas(Stack_lib lib){
    Libro aux;
    int i,j, max_pag=0;
    for(i=0;i<5;i++){
        aux=lib[i];
        for(j=i;j>0 && lib[j-1].getCant_de_pag()>aux.getCant_de_pag();j--){
            lib[j] = lib[j-1];
        }
        lib[j] = aux;
    }

    cout <<"La lista de libros ordenada queda: "<<endl;
    for(i=0;i<5;i++){
        cout <<i<<".- Titulo: "<<lib[i].getTitulo()<<" con "<<lib[i].getCant_de_pag()<<" paginas."<<endl;
    }
}
