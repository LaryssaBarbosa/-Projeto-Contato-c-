//# -Projeto-Contato-c-
//elaboração do projeto contato c++ , 28/04/2025 codigo-


#include <iostream>
#include <string>
using namespace std;


bool nomeValido(string nome) {
    for (char c : nome) {
        if (!isalpha(c) && c != ' ') { //verifica se tem letra 
            return false;
        }
    }
    return true;
}

// Função para validar se o email termina com @gmail.com
bool emailValido(string email) {
    string final = "@gmail.com";
    if (email.length() < final.length()) {
        return false;
    }
    string parteFinal = email.substr(email.length() - final.length());
    return parteFinal == final;
}


class Data {
private:
    int dia;
    int mes;
    int ano;
public:
    Data() {
        dia = 1;
        mes = 1;
        ano = 2006;
    }

    Data(int d, int m, int a) {
        dia = d;
        mes = m;
        ano = a;
    }

    int getDia() { return dia; }
    int getMes() { return mes; }
    int getAno() { return ano; }

    void setDia(int d) { dia = d; }
    void setMes(int m) { mes = m; }
    void setAno(int a) { ano = a; }
};


class Contato {
private:
    string email;
    string nome;
    string telefone;
    Data dtnasc;

public:
    Contato() {} 

    Contato(string n, string e, string t, Data d) {
        nome = n;
        email = e;
        telefone = t;
        dtnasc = d;
    }

    string getNome() { return nome; }
    string getEmail() { return email; }
    string getTelefone() { return telefone; }
    Data getData() { return dtnasc; }

    void setNome(string n) { nome = n; }
    void setEmail(string e) { email = e; }
    void setTelefone(string t) { telefone = t; }
    void setData(Data d) { dtnasc = d; }

    int idade() {
        int anoAtual = 2025;
        return anoAtual - dtnasc.getAno();
    }
};


int main() {
    Contato contatos[5];

    for (int i = 0; i < 5; i++) {
        string nome, email, telefone;
        int dia, mes, ano;

        cout << "Digite o nome do contato " << i + 1 << ": ";
        getline(cin, nome);
        while (!nomeValido(nome)) {
            cout << "Nome inválido! Digite apenas letras e espaços: ";
            getline(cin, nome);
        }

        cout << "Digite o email do contato " << i + 1 << ": ";
        getline(cin, email);
        while (!emailValido(email)) {
            cout << "Email invallido! Deve terminar com @gmail.com. Digite novamente: ";
            getline(cin, email);
        }

        cout << "Digite o telefone (com DDD) do contato " << i + 1 << ": ";
        getline(cin, telefone);
        while (telefone.length() != 11) {
            cout << "Telefone invalido! Deve ter exatamente 11 dígitos. Digite novamente: ";
            getline(cin, telefone);
        }

        cout << "Digite o dia de nascimento: ";
        cin >> dia;
        while (dia < 1 || dia > 31) {
            cout << "Dia inválido! Digite novamente (1 a 31): ";
            cin >> dia;
        }

        cout << "Digite o mês de nascimento: ";
        cin >> mes;
        while (mes < 1 || mes > 12) {
            cout << "Mês inválido! Digite novamente (1 a 12): ";
            cin >> mes;
        }

        cout << "Digite o ano de nascimento: ";
        cin >> ano;
        while (ano < 1925 || ano > 2025) {
            cout << "Ano inválido! Deve estar entre 1925 e 2025. Digite novamente: ";
            cin >> ano;
        }

        cin.ignore(); 

        Data dtnasc(dia, mes, ano);
        contatos[i] = Contato(nome, email, telefone, dtnasc);

        cout << endl;
    }

    cout << "\n--- Contatos Cadastrados ---\n";
    for (int i = 0; i < 5; i++) {
        cout << "Nome: " << contatos[i].getNome() << endl;
        cout << "Email: " << contatos[i].getEmail() << endl;
        cout << "Telefone: " << contatos[i].getTelefone() << endl;
        cout << "Idade: " << contatos[i].idade() << " anos" << endl;
        cout << "---------------------------\n";
    }

    return 0;
}
