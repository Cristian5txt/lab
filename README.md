#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Pago {
    int codigo;
    string nombre;
    string mes;
    double valor;
    string numeroCuenta;
};

vector<Pago> pagos;

void agregarPago() {
    Pago nuevoPago;
    cout << "Ingrese Código: ";
    cin >> nuevoPago.codigo;
    cin.ignore();
    cout << "Ingrese Nombre: ";
    getline(cin, nuevoPago.nombre);
    cout << "Ingrese Mes de Pago: ";
    getline(cin, nuevoPago.mes);
    cout << "Ingrese Valor del Pago: ";
    cin >> nuevoPago.valor;
    cin.ignore();
    cout << "Ingrese Número de Cuenta: ";
    getline(cin, nuevoPago.numeroCuenta);
    pagos.push_back(nuevoPago);
    cout << "Pago registrado correctamente!\n";
}

void listarPagos() {
    if (pagos.empty()) {
        cout << "No hay pagos registrados.\n";
        return;
    }
    for (const auto &pago : pagos) {
        cout << "Codigo: " << pago.codigo << ", Nombre: " << pago.nombre
             << ", Mes: " << pago.mes << ", Valor: " << pago.valor
             << ", Cuenta: " << pago.numeroCuenta << "\n";
    }
}

void consultarPorMes() {
    string mes;
    cout << "Ingrese el mes a consultar: ";
    cin.ignore();
    getline(cin, mes);
    double total = 0;
    for (const auto &pago : pagos) {
        if (pago.mes == mes) {
            total += pago.valor;
        }
    }
    cout << "Total de pagos en " << mes << ": " << total << "\n";
}

void consultarPorCodigo() {
    int codigo;
    cout << "Ingrese el código de usuario: ";
    cin >> codigo;
    bool encontrado = false;
    for (const auto &pago : pagos) {
        if (pago.codigo == codigo) {
            cout << "Mes: " << pago.mes << ", Valor: " << pago.valor << "\n";
            encontrado = true;
        }
    }
    if (!encontrado) {
        cout << "No se encontraron pagos para este código.\n";
    }
}

void actualizarPago() {
    int codigo;
    cout << "Ingrese el código del pago a actualizar: ";
    cin >> codigo;
    cin.ignore();
    for (auto &pago : pagos) {
        if (pago.codigo == codigo) {
            cout << "Ingrese Nuevo Nombre: ";
            getline(cin, pago.nombre);
            cout << "Ingrese Nuevo Mes: ";
            getline(cin, pago.mes);
            cout << "Ingrese Nuevo Valor: ";
            cin >> pago.valor;
            cin.ignore();
            cout << "Ingrese Nuevo Número de Cuenta: ";
            getline(cin, pago.numeroCuenta);
            cout << "Pago actualizado correctamente!\n";
            return;
        }
    }
    cout << "Código no encontrado.\n";
}

void eliminarPago() {
    int codigo;
    cout << "Ingrese el código del pago a eliminar: ";
    cin >> codigo;
    for (auto it = pagos.begin(); it != pagos.end(); ++it) {
        if (it->codigo == codigo) {
            pagos.erase(it);
            cout << "Pago eliminado correctamente!\n";
            return;
        }
    }
    cout << "Código no encontrado.\n";
}

void mostrarMenu() {
    int opcion;
    do {
        cout << "\n--- Sistema de Pagos ---\n";
        cout << "1. Registrar un pago\n";
        cout << "2. Consultar pagos por mes\n";
        cout << "3. Consultar pagos por código de usuario\n";
        cout << "4. Listar todos los pagos\n";
        cout << "5. Actualizar un pago\n";
        cout << "6. Eliminar un pago\n";
        cout << "7. Salir\n";
        cout << "Seleccione una opción: ";
        cin >> opcion;

        switch (opcion) {
            case 1: agregarPago(); break;
            case 2: consultarPorMes(); break;
            case 3: consultarPorCodigo(); break;
            case 4: listarPagos(); break;
            case 5: actualizarPago(); break;
            case 6: eliminarPago(); break;
            case 7: cout << "Saliendo...\n"; break;
            default: cout << "Opción inválida. Intente de nuevo.\n";
        }
    } while (opcion != 7);
}

int main() {
    mostrarMenu();
    return 0;
}
