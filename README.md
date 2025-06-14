import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Account {
    String accountNumber;
    String accountHolderName;
    double balance;

    public Account(String accountNumber, String accountHolderName, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolderName = accountHolderName;
        this.balance = balance;
    }
}

public class BankApplication {
    static Map<String, Account> accounts = new HashMap<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        while (true) {
            System.out.println("Bank Application");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Check Balance");
            System.out.println("5. Exit");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            switch (choice) {
                case 1:
                    createAccount();
                    break;
                case 2:
                    deposit();
                    break;
                case 3:
                    withdraw();
                    break;
                case 4:
                    checkBalance();
                    break;
                case 5:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice");
            }
        }
    }

    static void createAccount() {
        System.out.print("Enter account number: ");
        String accountNumber = scanner.nextLine();
        System.out.print("Enter account holder name: ");
        String accountHolderName = scanner.nextLine();
        System.out.print("Enter initial balance: ");
        double balance = scanner.nextDouble();
        scanner.nextLine(); // Consume newline left-over

        accounts.put(accountNumber, new Account(accountNumber, accountHolderName, balance));
        System.out.println("Account created successfully");
    }

    static void deposit() {
        System.out.print("Enter account number: ");
        String accountNumber = scanner.nextLine();
        System.out.print("Enter amount to deposit: ");
        double amount = scanner.nextDouble();
        scanner.nextLine(); // Consume newline left-over

        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            account.balance += amount;
            System.out.println("Deposit successful. New balance: " + account.balance);
        } else {
            System.out.println("Account not found");
        }
    }

    static void withdraw() {
        System.out.print("Enter account number: ");
        String accountNumber = scanner.nextLine();
        System.out.print("Enter amount to withdraw: ");
        double amount = scanner.nextDouble();
        scanner.nextLine(); // Consume newline left-over

        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            if (account.balance >= amount) {
                account.balance -= amount;
                System.out.println("Withdrawal successful. New balance: " + account.balance);
            } else {
                System.out.println("Insufficient balance");
            }
        } else {
            System.out.println("Account not found");
        }
    }

    static void checkBalance() {
        System.out.print("Enter account number: ");
        String accountNumber = scanner.nextLine();

        if (accounts.containsKey(accountNumber)) {
            Account account = accounts.get(accountNumber);
            System.out.println("Balance: " + account.balance);
        } else {
            System.out.println("Account not found");
        }
    }
}
