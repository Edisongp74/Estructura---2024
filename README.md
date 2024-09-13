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



juego agalludo
#include <iostream>
#include <ctime>
#include <cstdlib>
#include <fstream>
#include <string>

using namespace std;

// Clase para representar un jugador
class Player {
public:
    string name;
    int score;

    // Constructor para inicializar el nombre y la puntuación del jugador
    Player(const string& name) : name(name), score(0) {}

    // Método para aumentar la puntuación del jugador
    void increaseScore() {
        score++;
    }
};

// Clase para representar el juego de Agalludo
class Agalludo {
public:
    Player player1;
    Player player2;
    int currentPlayer; // 1 o 2 para indicar el jugador actual

    // Constructor para inicializar el juego
    Agalludo(const string& player1Name, const string& player2Name) 
        : player1(player1Name), player2(player2Name), currentPlayer(1) {}

    // Método para jugar una ronda del juego
    void playRound() {
        cout << "Turno de " << (currentPlayer == 1 ? player1.name : player2.name) << endl;

        int roll = rand() % 6 + 1;
        cout << "Lanzó un " << roll << endl;

        if (currentPlayer == 1) {
            player1.increaseScore();
        } else {
            player2.increaseScore();
        }

        showGameState();

        cout << "Desea seguir jugando (s/n)? ";
        char choice;
        cin >> choice;

        if (choice == 'n') {
            currentPlayer = (currentPlayer == 1) ? 2 : 1; // Cambiar jugador
        }
    }

    // Método para mostrar el estado actual del juego
    void showGameState() {
        cout << player1.name << ": " << player1.score << endl;
        cout << player2.name << ": " << player2.score << endl;
    }

    // Método para determinar el ganador del juego
    Player getWinner() {
        if (player1.score > player2.score) {
            return player1;
        } else if (player2.score > player1.score) {
            return player2;
        } else {
            return (currentPlayer == 1) ? player1 : player2;
        }
    }

    // Método para guardar el estado del juego en un archivo
    void saveGame(const string& filename) {
        ofstream outfile(filename);
        if (outfile.is_open()) {
            outfile << player1.name << endl;
            outfile << player1.score << endl;
            outfile << player2.name << endl;
            outfile << player2.score << endl;
            outfile << currentPlayer << endl;
            outfile.close();
            cout << "Juego guardado correctamente en " << filename << endl;
        } else {
            cout << "Error al guardar el juego." << endl;
        }
    }

    // Método para cargar el estado del juego desde un archivo
    void loadGame(const string& filename) {
        ifstream infile(filename);
        if (infile.is_open()) {
            getline(infile, player1.name);
            infile >> player1.score;
            getline(infile, player2.name);
            infile >> player2.score;
            infile >> currentPlayer;
            infile.close();
            cout << "Juego cargado correctamente desde " << filename << endl;
        } else {
            cout << "Error al cargar el juego." << endl;
        }
    }
};

int main() {
    srand(time(0));

    // Solicitar nombres de los jugadores
    string player1Name, player2Name;
    cout << "Ingrese el nombre del jugador 1: ";
    cin >> player1Name;
    cout << "Ingrese el nombre del jugador 2: ";
    cin >> player2Name;

    Agalludo game(player1Name, player2Name); // Crea el objeto Agalludo con los nombres

    // Comprobar si existe un juego guardado
    string savedGameFile = "saved_game.txt";
    ifstream infile(savedGameFile);
    if (infile.is_open()) {
        cout << "Se encontró un juego guardado. Cargando..." << endl;
        game.loadGame(savedGameFile);
        infile.close();
    } 

    // Bucle principal del juego
    while (true) {
        // Jugar rondas hasta que un jugador alcance 10 puntos
        while (game.player1.score < 10 && game.player2.score < 10) {
            game.playRound();
            cout << endl;
        }

        // Mostrar el ganador
        Player winner = game.getWinner();
        cout << "El ganador es " << winner.name << "!" << endl;

        // Preguntar si se desea guardar el juego
        cout << "Desea guardar el juego (s/n)? ";
        char choice;
        cin >> choice;
        if (choice == 's') {
            game.saveGame(savedGameFile);
        }

        // Preguntar si se desea jugar de nuevo
        cout << "Desea jugar de nuevo (s/n)? ";
        cin >> choice;
        if (choice == 'n') {
            break;
        } else {
            game = Agalludo(game.player1.name, game.player2.name); // Crea un nuevo juego con los mismos nombres
        }
    }

    return 0;
}




https://replit.com/join/ugwamkccxu-sebasch510

