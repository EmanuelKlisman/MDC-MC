

// DUPLA:

// Ícaro Rebouças Pinheiro
//  Emanuel Klisman do Nascimento Nogueira

// DATA: (07/09/2024)
// Turma: ADS - VIA CORPVS - NOITE

#include <iostream>
#include <limits>
#include <locale>
// Manipulação de Caracteres:
#include <cctype>
// Para armazenar valores dinâmicos:
#include <vector>
using namespace std;

// MDC (algoritmo de Euclides):
int calcMDC(int a, int b)
{
    // Enquanto o valor for diferente de zero:
    while (b != 0)
    {
        // Armazenar temporariamente.
        int temp = b;
        // Resto da divisão de um pelo outro.
        b = a % b;
        a = temp;
    }
    return a;
}

// MMC:
int calcMMC(int a, int b)
{
    // MMC será a divisão da multiplicação dos valores pelo MDC dos mesmos:
    return (a * b) / calcMDC(a, b);
}

int main()
{
    // Array dinâmico:
    vector<int> valores;

    // Resposta (S / N):
    string resp;

    // Valor inserido:
    int valor;

    // Estrutura DO WHILE -> executar pelo menos uma vez:
    do
    {
        // Leitura do valor:
        cout << "Digite um valor: ";

        // Enquanto a entrada não for um número válido
        while (!(cin >> valor))
        {
            cout << "Erro: Digite um valor inteiro!" << endl;
            cin.clear();                                         // Limpa o estado de erro
            cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Ignora a entrada inválida
        }

        valores.push_back(valor);
        // Validação da resposta (S/N):
        do
        {
            cout << "Deseja inserir mais algum valor? (S/N): ";
            cin >> resp;

            // Converte a resposta para minúsculas (s/n):
            for (char &c : resp)
            {
                c = tolower(c);
            }

            if (resp != "s" && resp != "n")
            {
                cout << "Erro: Responda apenas com 'S' ou 'N'!" << endl;
            }
        } while (resp != "s" && resp != "n");

    } while (resp == "S" || resp == "s");

    // Se for mais de um valor:
    if (valores.size() > 1)
    {
        // MMC e MDC dos valores informados (4, 10 E 12)
        int valMMC = valores[0]; // 4
        int valMDC = valores[0]; // 4

        for (size_t i = 1; i < valores.size(); i++)
        {
            valMMC = calcMMC(valMMC, valores[i]);
            valMDC = calcMDC(valMDC, valores[i]);
        }

        cout << "MMC dos valores informados: " << valMMC << endl;
        cout << "MDC dos valores informados: " << valMDC << endl;
    }

    // Se for apenas um valor:
    else if (valores.size() == 1)
    {
        // No caso de um único valor, o MMC e o MDC são iguais:

        cout << "Somente um valor foi inserido! " << valores[0] << endl;
        cout << "MMC e MDC: " << valores[0] << endl;
    }
    else
    {
        cout << "Nenhum valor inserido!" << endl;
    }

    return 0;
}
