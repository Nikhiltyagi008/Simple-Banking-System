// BankAccount class
class BankAccount {
    private int accountNumber;
    private double balance;

    public BankAccount(int accountNumber, double initialBalance) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }

    public int getAccountNumber() {
        return accountNumber;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Successfully deposited " + amount + ". New balance: " + balance);
        } else {
            System.out.println("Deposit amount must be positive.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0) {
            if (balance >= amount) {
                balance -= amount;
                System.out.println("Successfully withdrew " + amount + ". New balance: " + balance);
            } else {
                System.out.println("Insufficient funds. Available balance: " + balance);
            }
        } else {
            System.out.println("Withdrawal amount must be positive.");
        }
    }
}

// Customer class
class Customer {
    private String name;
    private ArrayList<BankAccount> accounts;

    public Customer(String name) {
        this.name = name;
        this.accounts = new ArrayList<>();
    }

    public BankAccount openAccount(double initialBalance) {
        int accountNumber = accounts.size() + 1;
        BankAccount newAccount = new BankAccount(accountNumber, initialBalance);
        accounts.add(newAccount);
        System.out.println("Account " + accountNumber + " opened with initial balance " + initialBalance);
        return newAccount;
    }

    public BankAccount getAccount(int accountNumber) {
        for (BankAccount account : accounts) {
            if (account.getAccountNumber() == accountNumber) {
                return account;
            }
        }
        System.out.println("Account not found.");
        return null;
    }
}

// Main class for testing
public class Main {
    public static void main(String[] args) {
        Customer customer = new Customer("John Doe");

        // Open new account
        BankAccount account = customer.openAccount(500);

        // Deposit money
        account.deposit(200);

        // Withdraw money
        account.withdraw(100);

        // Check balance
        System.out.println("Current balance: " + account.getBalance());
    }
}
