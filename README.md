import json
import os

# File to store expenses
EXPENSE_FILE = "expenses.json"

def load_expenses():
    if os.path.exists(EXPENSE_FILE):
        with open(EXPENSE_FILE, 'r') as file:
            return json.load(file)
    return []

def save_expenses(expenses):
    with open(EXPENSE_FILE, 'w') as file:
        json.dump(expenses, file)

def add_expense(expenses):
    amount = float(input("Enter amount spent: "))
    description = input("Enter a brief description: ")
    category = input("Enter category (Food, Transportation, Entertainment): ")
    expense = {
        "amount": amount,
        "description": description,
        "category": category
    }
    expenses.append(expense)
    save_expenses(expenses)
    print("Expense added successfully.")

def view_summary(expenses):
    total = sum(expense['amount'] for expense in expenses)
    print(f"Total expenses: ${total:.2f}")
    
    categories = {}
    for expense in expenses:
        category = expense['category']
        if category in categories:
            categories[category] += expense['amount']
        else:
            categories[category] = expense['amount']
    
    for category, amount in categories.items():
        print(f"{category}: ${amount:.2f}")

def main():
    expenses = load_expenses()
    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. View Summary")
        print("3. Exit")
        choice = input("Choose an option: ")
        
        if choice == '1':
            add_expense(expenses)
        elif choice == '2':
            view_summary(expenses)
        elif choice == '3':
            break
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()
