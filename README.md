# Tarea-orga-CI-23641930
#include <iostream>
#include <string>
#include <stdio.h>


using namespace std;
struct poderes
{
	char nombrepoder[20];	
	int iD;
};

class node  //definición del nodo de la lista
{
public:
	char nombre[18];
  	int edad;
	int poder;
	int numpoder; 
  	poderes nompoder[100];
  	char descripcion[1000];
  	node *sig;
  	node *ant;
	
	node()
	{
		//Debo crear los arreglos aqui adentro tambien o que?
		edad = poder = numpoder=0; 
		ant=sig=NULL;
	}
	void RellenarNodo()
	{
		node* a= new node();

		cin>>a->nombre;
		cout<<"entro"<<endl;
		cin >> a->edad >> a->poder >> a->numpoder;
		for(int i=0; i<a->numpoder;i++)
		{
			cin >> a->nompoder[i].nombrepoder;
			cin>>nompoder[i].iD;
		}
		int x=0;
		scanf("%c", &a->descripcion[x]);
		do
		{
			x++;
			scanf("%c", &a->descripcion[x]);
		}while(a->descripcion[x]!='\n');
		a->sig=a->ant=NULL;
	}
	
};

template <class T>
class Lista
{	
public:
	typedef node* tposition;

private:
	tposition pfirst, plast;
	int in;
	
public:
	
	Lista()
	{
		in=0;
		pfirst=plast= NULL;
	}
	~Lista()
	{
		node *ptemp;
		while (pfirst != 0){
			ptemp=pfirst;
			pfirst=pfirst->sig;
			delete ptemp;
		}
	}
	
	bool IsEmpty()
	{
		return (pfirst == 0);
	}	
 
	tposition First(){
		return pfirst;
	}
	tposition Last(){
	    return plast;	
	}
	void Next(tposition &pvalue){
	    pvalue=pvalue->sig;
	}
	void Prev(tposition &pvalue)
	{
		if(!IsEmpty() && pvalue != NULL)
        {
            pvalue = pvalue->ant;
        }
	}
	//Usar en la forma b nada mas! a la hora de comparar
	/*
	T get(tposition pvalue)
	{
	    return ();	
	}
	*/
	//Corregirrr si falla
	
	void FormaPeliminar()
	{
		tposition temp=pfirst;
		pfirst=pfirst->sig;	
		pfirst->ant=NULL;
		in=in-1;
		delete temp;
	}
	void FormaPinsertar(node* y)
	{
		in=in+1;
		y->RellenarNodo();
		y->sig=pfirst;
		y->ant= NULL;
		pfirst=y;
		
	}
	void InsertarUltimo(node* x)
	{
		x->RellenarNodo();
		x->sig=NULL;
		if (pfirst==NULL)
		{
			pfirst=x;
		}
		else
		{
			plast->sig=x;
			x->ant=plast;
		}
		plast=x;
		in=in+1;
	}
	void EliminarUltimo()
	{
		node* temp=plast;
		plast=plast->ant;
		plast->sig=NULL;
		delete temp;
		in=in-1;
	}
	void ordenarLista(Lista &actual)
	{
		tposition siguiente,anterior;
		while(actual->sig!=NULL)
		{
			siguiente=actual->sig;  
			while(siguiente!=NULL)
			{
				for(int i=0;i<in;i++)
				{
					for(int j=i+1;j<=in;j++)
					{
						if(strcmp(actual->nombre[i], actual->nombre[j]) > 0)
						{
							siguiente*actual->nombre[i]=siguiente*actual->nombre[j];	
							siguiente*actual->nombre[j]=actual->nombre[i];
							anterior*actual->nombre[i]=actual->nombre[j];
							anterior->sig->nombre[i]=actual->nombre[i];
						}
					}
				} 
				siguiente=siguiente->sig;                    
			}    
			actual=actual->sig;
			siguiente=actual->sig;   
		}
	}	
};

int main (){
	Lista<node>* Guerrero= new Lista<node>();
	int n;
	cin>>n;
	for(int i=0;i<n;i++)
	{
		node* inicial= new node();
		Guerrero->InsertarUltimo(inicial);
		cout<<endl<<"retorno"<<endl;
	}
	cout<<"termino de leer los primeros guerreros"<<endl;
	int nf;
	cin>>nf;
	int c=0,pasos;
	char forma[7];
	char ins[8];
	node* in=new node();
	for (c=0;c<nf;c++)
	{
		cin>>forma;
		cout<<"introduzca numero de pasos a realizar"<<endl;
		cin>>pasos;
		if(forma[6]=='P')
		{
			for(int g=0;g<pasos;g++)
			{
				cin>>ins;
				if (ins[0]=='I'|| ins[0]=='i')
				{
					Guerrero->FormaPinsertar(in);
				}
				if (ins[0]=='E'|| ins[0]=='e')
				{
					Guerrero->FormaPeliminar();
				}
			}
		}
		if(forma[6]=='C')
		{
			for(int g=0;g<pasos;g++)
			{
				cin>>ins;
				if (ins[0]=='I'|| ins[0]=='i')
				{
					Guerrero->InsertarUltimo(in);
				}
				if (ins[0]=='E'|| ins[0]=='e')
				{
					Guerrero->FormaPeliminar();
				}
			}
		}
		if(forma[6]=='D')
		{
			for(int g=0;g<pasos;g++)
			{
				cin>>ins;
				if (ins[0]=='I'|| ins[0]=='i')
				{
					cin>>ins;
					if(ins[1]=='r')
					{
						Guerrero->FormaPinsertar(in);
					}
					else
					{
							Guerrero->InsertarUltimo(in);
					}
				}
				if (ins[0]=='E'|| ins[0]=='e')
				{
					cin>>ins;
					if(ins[1]=='r')
					{
						Guerrero->FormaPeliminar();
					}
					else
					{
						Guerrero->EliminarUltimo();
					}
				}
			}
				//llamar a ordenar Lista::ordenarLista(Guerrero);
		}
		//falta forma B
	}
	Guerrero->~Lista();
	return 0;
}
