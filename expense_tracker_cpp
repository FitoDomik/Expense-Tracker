#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
#include <limits>

struct Expense {
    double amount;
    std::string description;
    int id;
    
    // Конструктор
    Expense(double amt, const std::string& desc, int identifier) 
        : amount(amt), description(desc), id(identifier) {}
};

class ExpenseTracker {
private:
    std::vector<Expense> expenses;
    int nextId;
    
public:
    ExpenseTracker() : nextId(1) {}
    
    void run() {
        std::cout << "=== 💰 КАЛЬКУЛЯТОР РАСХОДОВ ===\n";
        std::cout << "Добро пожаловать в трекер расходов!\n";
        
        int choice;
        do {
            showMenu();
            choice = getChoice();
            
            switch (choice) {
                case 1:
                    addExpense();
                    break;
                case 2:
                    showExpenses();
                    break;
                case 3:
                    showTotal();
                    break;
                case 4:
                    deleteExpense();
                    break;
                case 5:
                    showStatistics();
                    break;
                case 6:
                    std::cout << "\nСпасибо за использование! До свидания! 👋\n";
                    break;
                default:
                    std::cout << "❌ Неверный выбор. Попробуйте снова.\n";
            }
            
            if (choice != 6) {
                std::cout << "\nНажмите Enter для продолжения...";
                std::cin.ignore();
                std::cin.get();
                std::cout << "\n";
            }
            
        } while (choice != 6);
    }
    
private:
    void showMenu() {
        std::cout << "--- МЕНЮ ---\n";
        std::cout << "1. ➕ Добавить расход\n";
        std::cout << "2. 📄 Показать все расходы\n";
        std::cout << "3. 💰 Общая сумма расходов\n";
        std::cout << "4. 🗑️  Удалить расход\n";
        std::cout << "5. 📊 Статистика\n";
        std::cout << "6. ❌ Выход\n";
        std::cout << "Выберите действие (1-6): ";
    }
    
    int getChoice() {
        int choice;
        while (!(std::cin >> choice)) {
            std::cout << "❌ Введите число от 1 до 6: ";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        }
        std::cin.ignore(); // Очистка буфера
        return choice;
    }
    
    void addExpense() {
        double amount;
        std::string description;
        
        std::cout << "\n--- ДОБАВЛЕНИЕ РАСХОДА ---\n";
        
        // Ввод суммы
        std::cout << "Введите сумму расхода: ";
        while (!(std::cin >> amount) || amount < 0) {
            std::cout << "❌ Введите корректную сумму (больше 0): ";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        }
        std::cin.ignore(); // Очистка буфера
        
        // Ввод описания
        std::cout << "Введите описание расхода: ";
        std::getline(std::cin, description);
        
        if (description.empty()) {
            description = "Без описания";
        }
        
        // Добавление расхода
        expenses.emplace_back(amount, description, nextId++);
        
        std::cout << "✅ Расход добавлен успешно!\n";
        std::cout << "💳 Сумма: " << std::fixed << std::setprecision(2) << amount << " руб.\n";
        std::cout << "📝 Описание: " << description << "\n";
    }
    
    void showExpenses() {
        std::cout << "\n--- СПИСОК РАСХОДОВ ---\n";
        
        if (expenses.empty()) {
            std::cout << "📭 Список расходов пуст. Добавьте первый расход!\n";
            return;
        }
        
        std::cout << std::left << std::setw(5) << "ID" 
                  << std::setw(12) << "Сумма" 
                  << "Описание\n";
        std::cout << std::string(50, '-') << "\n";
        
        for (const auto& expense : expenses) {
            std::cout << std::left << std::setw(5) << expense.id
                      << std::setw(12) << std::fixed << std::setprecision(2) 
                      << (std::to_string(expense.amount) + " руб.")
                      << expense.description << "\n";
        }
    }
    
    void showTotal() {
        std::cout << "\n--- ОБЩАЯ СУММА РАСХОДОВ ---\n";
        
        if (expenses.empty()) {
            std::cout << "📭 Нет расходов для подсчета.\n";
            return;
        }
        
        double total = 0.0;
        for (const auto& expense : expenses) {
            total += expense.amount;
        }
        
        std::cout << "💰 Общая сумма расходов: " << std::fixed << std::setprecision(2) 
                  << total << " руб.\n";
        std::cout << "📊 Количество записей: " << expenses.size() << "\n";
        
        if (!expenses.empty()) {
            double average = total / expenses.size();
            std::cout << "📈 Средний расход: " << std::fixed << std::setprecision(2) 
                      << average << " руб.\n";
        }
    }
    
    void deleteExpense() {
        std::cout << "\n--- УДАЛЕНИЕ РАСХОДА ---\n";
        
        if (expenses.empty()) {
            std::cout << "📭 Нет расходов для удаления.\n";
            return;
        }
        
        showExpenses();
        
        int id;
        std::cout << "\nВведите ID расхода для удаления: ";
        while (!(std::cin >> id)) {
            std::cout << "❌ Введите корректный ID: ";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        }
        
        // Поиск и удаление расхода
        auto it = std::find_if(expenses.begin(), expenses.end(),
                              [id](const Expense& expense) {
                                  return expense.id == id;
                              });
        
        if (it != expenses.end()) {
            std::cout << "🗑️  Удален расход: " << it->description 
                      << " (" << std::fixed << std::setprecision(2) 
                      << it->amount << " руб.)\n";
            expenses.erase(it);
        } else {
            std::cout << "❌ Расход с ID " << id << " не найден.\n";
        }
    }
    
    void showStatistics() {
        std::cout << "\n--- 📊 СТАТИСТИКА РАСХОДОВ ---\n";
        
        if (expenses.empty()) {
            std::cout << "📭 Нет данных для анализа.\n";
            return;
        }
        
        double total = 0.0;
        double maxExpense = expenses[0].amount;
        double minExpense = expenses[0].amount;
        std::string maxDescription = expenses[0].description;
        std::string minDescription = expenses[0].description;
        
        for (const auto& expense : expenses) {
            total += expense.amount;
            
            if (expense.amount > maxExpense) {
                maxExpense = expense.amount;
                maxDescription = expense.description;
            }
            
            if (expense.amount < minExpense) {
                minExpense = expense.amount;
                minDescription = expense.description;
            }
        }
        
        double average = total / expenses.size();
        
        std::cout << "📋 Всего записей: " << expenses.size() << "\n";
        std::cout << "💰 Общая сумма: " << std::fixed << std::setprecision(2) 
                  << total << " руб.\n";
        std::cout << "📈 Средний расход: " << std::fixed << std::setprecision(2) 
                  << average << " руб.\n";
        std::cout << "⬆️  Максимальный расход: " << std::fixed << std::setprecision(2) 
                  << maxExpense << " руб. (" << maxDescription << ")\n";
        std::cout << "⬇️  Минимальный расход: " << std::fixed << std::setprecision(2) 
                  << minExpense << " руб. (" << minDescription << ")\n";
        
        // Анализ трат
        if (total > 10000) {
            std::cout << "⚠️  Внимание: большие траты за период!\n";
        } else if (total < 1000) {
            std::cout << "👍 Отличный контроль расходов!\n";
        } else {
            std::cout << "💡 Умеренные расходы.\n";
        }
    }
};

int main() {
    // Установка локали для корректного отображения русского текста
    setlocale(LC_ALL, "Russian");
    
    ExpenseTracker tracker;
    tracker.run();
    
    return 0;
}
