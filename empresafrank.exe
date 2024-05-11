#include <iostream>
#include <limits>

using namespace std;

struct RNT {
    char nombreEmpresa[20];
    int codigo;
    int fechadevencimiento;
    RNT *izq;
    RNT *der;
};

RNT *raizPorFecha = nullptr;
RNT *raizPorCodigo = nullptr;
RNT *auxPorCodigo = nullptr;
RNT *auxPorFecha = nullptr;
RNT *auxPorCodigo2 = nullptr;
RNT *auxPorFecha2 = nullptr;

void registrarEmpresa();
void posicionarPorCodigo();
void posicionarPorFecha();
void mostrarInOrden(RNT *recursive);
void mostrarPreOrden(RNT *recursive);
void mostrarPostOrden(RNT *recursive);
void eliminarPorCodigo(RNT *&arbol, int codigo);
RNT *encontrarSucesor(RNT *nodo);

void registrarEmpresa() {
    RNT *nuevo = new RNT;

    cout << "Ingrese el nombre de la empresa: ";
    cin.ignore(); 
    cin.getline(nuevo->nombreEmpresa, 20);
    cout << "Ingrese el codigo: ";
    cin >> nuevo->codigo;
    cout << "Ingrese la fecha de vencimiento: ";
    cin >> nuevo->fechadevencimiento;

    nuevo->izq = nullptr;
    nuevo->der = nullptr;

    if (raizPorCodigo == nullptr) {
        raizPorCodigo = nuevo;
        raizPorFecha = nuevo;
    } else {
        auxPorCodigo = raizPorCodigo;
        auxPorFecha = raizPorFecha;
        posicionarPorCodigo();
        posicionarPorFecha();
    }
}

void posicionarPorCodigo() {
    while (true) {
        if (auxPorCodigo->codigo < auxPorCodigo2->codigo) {
            if (auxPorCodigo2->izq != nullptr) {
                auxPorCodigo2 = auxPorCodigo2->izq;
            } else {
                auxPorCodigo2->izq = auxPorCodigo;
                break;
            }
        } else if (auxPorCodigo->codigo > auxPorCodigo2->codigo) {
            if (auxPorCodigo2->der != nullptr) {
                auxPorCodigo2 = auxPorCodigo2->der;
            } else {
                auxPorCodigo2->der = auxPorCodigo;
                break;
            }
        }
    }
}

void posicionarPorFecha() {
    while (true) {
        if (auxPorFecha->fechadevencimiento < auxPorFecha2->fechadevencimiento) {
            if (auxPorFecha2->izq != nullptr) {
                auxPorFecha2 = auxPorFecha2->izq;
            } else {
                auxPorFecha2->izq = auxPorFecha;
                break;
            }
        } else if (auxPorFecha->fechadevencimiento >= auxPorFecha2->fechadevencimiento) {
            if (auxPorFecha2->der != nullptr) {
                auxPorFecha2 = auxPorFecha2->der;
            } else {
                auxPorFecha2->der = auxPorFecha;
                break;
            }
        }
    }
}

void mostrarPreOrden(RNT *recursive) {
    if (recursive != nullptr) {
        cout << "Nombre: " << recursive->nombreEmpresa << endl;
        cout << "Codigo: " << recursive->codigo << endl;
        cout << "Fecha de vencimiento: " << recursive->fechadevencimiento << endl;
        mostrarPreOrden(recursive->izq);
        mostrarPreOrden(recursive->der);
    }
}

void mostrarInOrden(RNT *recursive) {
    if (recursive != nullptr) {
        mostrarInOrden(recursive->izq);
        cout << "Nombre: " << recursive->nombreEmpresa << endl;
        cout << "Codigo: " << recursive->codigo << endl;
        cout << "Fecha de vencimiento: " << recursive->fechadevencimiento << endl;
        mostrarInOrden(recursive->der);
    }
}

void mostrarPostOrden(RNT *recursive) {
    if (recursive != nullptr) {
        mostrarPostOrden(recursive->izq);
        mostrarPostOrden(recursive->der);
        cout << "Nombre: " << recursive->nombreEmpresa << endl;
        cout << "Codigo: " << recursive->codigo << endl;
        cout << "Fecha de vencimiento: " << recursive->fechadevencimiento << endl;
    }
}

RNT *encontrarSucesor(RNT *nodo) {
    RNT *actual = nodo;
    while (actual->izq != nullptr) {
        actual = actual->izq;
    }
    return actual;
}

void eliminarPorCodigo(RNT *&arbol, int codigo) {
    if (arbol == nullptr) {
        return;
    }
    if (codigo < arbol->codigo) {
        eliminarPorCodigo(arbol->izq, codigo);
    } else if (codigo > arbol->codigo) {
        eliminarPorCodigo(arbol->der, codigo);
    } else {
        if (arbol->izq == nullptr && arbol->der == nullptr) {
            delete arbol;
            arbol = nullptr;
        } else if (arbol->izq == nullptr) {
            RNT *temp = arbol;
            arbol = arbol->der;
            delete temp;
        } else if (arbol->der == nullptr) {
            RNT *temp = arbol;
            arbol = arbol->izq;
            delete temp;
        } else {
            RNT *sucesor = encontrarSucesor(arbol->der);
            arbol->codigo = sucesor->codigo;
            eliminarPorCodigo(arbol->der, sucesor->codigo);
        }
    }
}

int main() {
    int opcion;

    do {
        cout << "Menu:" << endl;
        cout << "1. Registrar Empresa" << endl;
        cout << "2. Eliminar Empresa" << endl;
        cout << "3. Recorrer PreOrden" << endl;
        cout << "4. Recorrer inOrden" << endl;
        cout << "5. Recorrer PostOrden" << endl;
        cout << "6. Salir" << endl;
        cout << "Opcion: ";
        cin >> opcion;
        cin.ignore(numeric_limits<streamsize>::max(), '\n');

        switch (opcion) {
            case 1:
                registrarEmpresa();
                break;
            case 2:
                int codigoAEliminar;
                cout << "Ingrese el codigo del estudiante a eliminar: ";
                cin >> codigoAEliminar;
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                eliminarPorCodigo(raizPorFecha, codigoAEliminar);
                eliminarPorCodigo(raizPorCodigo, codigoAEliminar);
                break;
            case 3:
                cout << "Arbol Codigos en preorden: " << endl;
                mostrarPreOrden(raizPorCodigo);
                cout << endl;
                cout << "Arbol Fechas en preorden: " << endl;
                mostrarPreOrden(raizPorFecha);
                break;
            case 4:
                cout << "Arbol Codigos en inorden: " << endl;
                mostrarInOrden(raizPorCodigo);
                cout << endl;
                cout << "Arbol Fechas en inorden: " << endl;
                mostrarInOrden(raizPorFecha);
                break;
            case 5:
                cout << "Arbol Codigos en postorden: " << endl;
                mostrarPostOrden(raizPorCodigo);
                cout << endl;
                cout << "Arbol Fechas en postorden: " << endl;
                mostrarPostOrden(raizPorFecha);
                break;
            case 6:
                exit(0);
                break;
            default:
                cout << "Opcion invalida. Intentalo de nuevo." << endl;
        }
    } while (opcion != 6);

    while (raizPorFecha != nullptr) {
        RNT *temp = raizPorFecha;
        raizPorFecha = raizPorFecha->izq;
        delete temp;
    }

    while (raizPorCodigo != nullptr) {
        RNT *temp = raizPorCodigo;
        raizPorCodigo = raizPorCodigo->izq;
        delete temp;
    }

    return 0;
}