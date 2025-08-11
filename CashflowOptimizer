#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

class Person {
public:
    string name;
    int balance;

    Person(string name, int balance) {
        this->name = name;
        this->balance = balance;
    }
};

class CashflowMinimizer {
private:
    vector<Person> people;

    // Get index of max creditor or debtor
    int getMaxIndex(bool isCreditor) {
        int idx = -1;
        int maxVal = isCreditor ? INT_MIN : INT_MAX;

        for (int i = 0; i < people.size(); ++i) {
            if (isCreditor && people[i].balance > maxVal) {
                maxVal = people[i].balance;
                idx = i;
            } else if (!isCreditor && people[i].balance < maxVal) {
                maxVal = people[i].balance;
                idx = i;
            }
        }
        return idx;
    }

public:
    CashflowMinimizer(const vector<Person>& persons) {
        this->people = persons;
    }

    void minimizeCashFlow() {
        vector<string> transactions;

        while (true) {
            int creditorIdx = getMaxIndex(true);
            int debtorIdx = getMaxIndex(false);

            if (creditorIdx == -1 || debtorIdx == -1 ||
                people[creditorIdx].balance == 0 || people[debtorIdx].balance == 0)
                break;

            int minAmount = min(people[creditorIdx].balance, -people[debtorIdx].balance);

            people[creditorIdx].balance -= minAmount;
            people[debtorIdx].balance += minAmount;

            string t = people[debtorIdx].name + " pays " + to_string(minAmount) +
                       " to " + people[creditorIdx].name;
            transactions.push_back(t);
        }

        // Print Transactions
        cout << "\nOptimal Transactions:\n";
        for (const string& t : transactions) {
            cout << t << endl;
        }
    }

    void printBalances(string title) {
        cout << "\n" << title << ":\n";
        for (const auto& p : people) {
            cout << p.name << ": " << p.balance << endl;
        }
    }
};

int main() {
    vector<Person> people = {
        Person("Alice", -100),
        Person("Bob", 50),
        Person("Charlie", 50)
    };

    CashflowMinimizer minimizer(people);

    minimizer.printBalances("Initial Balances");
    minimizer.minimizeCashFlow();
    minimizer.printBalances("Final Balances");

    return 0;
}
