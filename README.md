#include <iostream> 
#include <vector> 
#include <cmath> 
#include <windows.h> 

using namespace std;

int main() {
    SetConsoleCP(1251);
    SetConsoleOutputCP(1251);
    int n;
    cout << "Введите количество вещей: ";
    cin >> n;
    // Проверка ввода
    if (n <= 0) {
        cout << "Ошибка: количество вещей должно быть положительным числом." << endl;
        return 0;
    }

    vector<int> weights(n);
    int totalWeight = 0;
    cout << "Введите вес каждой вещи: ";
    for (int i = 0; i < n; ++i) {
        cin >> weights[i];

        // Проверка ввода
        if (weights[i] <= 0) {
            cout << "Ошибка: вес каждой вещи должен быть положительным числом." << endl;
            return 0;
        }

        totalWeight += weights[i];
    }

    int targetWeight = totalWeight / 2;
    vector<bool> dp(targetWeight + 1);
    dp[0] = true;

    // Используем динамическое программирование для нахождения возможных комбинаций весов
    for (int i = 0; i < n; ++i) {
        for (int j = targetWeight; j >= weights[i]; --j) {
            dp[j] = dp[j] || dp[j - weights[i]];
        }
    }

    int firstBackpackWeight = 0;
    for (int i = targetWeight; i > 0; --i) {
        if (dp[i]) {
            firstBackpackWeight = i;
            break;
        }
    }

    cout << "Вес рюкзака первого друга: " << firstBackpackWeight << endl;
    cout << "Вес рюкзака второго друга: " << totalWeight - firstBackpackWeight << endl;

    return 0;
}
