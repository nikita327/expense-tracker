# expense-tracker
import csv
import os
from datetime import datetime

EXPENSE_FILE = "expenses.csv"

def add_expense():
    date = datetime.now().strftime('%Y-%m-%d')
    category = input("Enter expense category (e.g., Food, Travel, Shopping): ")
    amount = float(input("Enter expense amount: "))
    description = input("Enter a short description: ")
    
    with open(EXPENSE_FILE, 'a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([date, category, amount, description])
    
    print("Expense added successfully!\n")

def view_expenses():
    if not os.path.exists(EXPENSE_FILE):
        print("No expenses recorded yet.\n")
        return
    
    with open(EXPENSE_FILE, 'r') as file:
        reader = csv.reader(file)
        print("Date        | Category   | Amount | Description")
        print("-" * 50)
        for row in reader:
            print(f"{row[0]} | {row[1]:<10} | {row[2]:<6} | {row[3]}")
    print("\n")

def total_expenses():
    if not os.path.exists(EXPENSE_FILE):
        print("No expenses recorded yet.\n")
        return
    
    total = 0.0
    with open(EXPENSE_FILE, 'r') as file:
        reader = csv.reader(file)
        for row in reader:
            total += float(row[2])
    
    print(f"Total Expenses: ₹{total:.2f}\n")

def main():
    while True:
        print("Expense Tracker")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Total Expenses")
        print("4. Exit")
        choice = input("Enter your choice: ")
        
        if choice == '1':
            add_expense()
        elif choice == '2':
            view_expenses()
        elif choice == '3':
            total_expenses()
        elif choice == '4':
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.\n")

if __name__ == "__main__":
    main()
