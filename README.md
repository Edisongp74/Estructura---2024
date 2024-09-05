# Estructura---2024

Listo
chocolisto
bestias
#que hpta cosa tan dura


#include <iostream>
#include <vector>

using namespace std ;


int main()
{
   
    vector<int> miVector;
    
    
    bool decision = true ;
    int valor;
    
    while(decision){
        cout<<"ingresar valor : "<<endl;
        cin>>valor;
        
        miVector.push_back(valor);
     cout<<"desea seguir ingresando 1/0" << endl ;
        cin>>decision;
       
    }
cout <<miVector.size() << endl;
    
    
    for(int i=0; i<miVector.size(); i++){
        
        cout<< "miVector[" << i <<"]"<<miVector[i] <<endl;
    }

    return 0;
}
