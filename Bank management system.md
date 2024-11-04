#include <iostream>
#include <fstream>
#include <sstream>
#include <vector>
#include <time.h>
#include <string>

using namespace std;

class Account {
public:
    string name;
    long long int acc_num;
    long long int phn_num;
    string email;
    string address;
    string DOB;
    int atm_pin;
    float amount = 0;
    float withdrawal;
    float deposit;

    void create_acc() {
        cout << "Enter the Account Holder name: ";
        fflush(stdin);
        getline(cin, name);
        cout << "Enter " << name << "'s Phone number: ";
        cin >> phn_num;
        cout << "Enter the Account Holder's email: ";
        fflush(stdin);
        getline(cin, email);
        cout << "Enter the Account Holder address: ";
        fflush(stdin);
        getline(cin, address);
        cout << "Enter the Account Holder DOB (date/month/year): ";
        fflush(stdin);
        cin >> DOB;
        acc_num = generate_acc();
    }

    long long int generate_acc() {
        long long int acc_n1;
        srand((long long int)time(NULL));
        acc_n1 = (rand() % 9000000000) + 1000000000;
        return acc_n1;
    }

    void showing_details1() {
        cout << "The Account Holder's name: " << name << endl;
        cout << "The Account Holder's Phone number: " << phn_num << endl;
        cout << "The Account Holder's email: " << email << endl;
        cout << "The Account Holder's Address: " << address << endl;
        cout << "The Account Holder's DOB: " << DOB << endl;
        cout << "Mr./Miss. " << name << ", Your account number is: " << acc_num << endl;
    }
    void show_acc(){
        cout << "Mr./Miss. " << name << ", Your account number is: " << acc_num << endl;
    }

    void save_file_create_acc() {
        ofstream file("Accounts_public.csv", ios::app);
        if (!file) {
            cout << "File could not open!!!" << endl;
        } else {
            file << name << "," << acc_num << "," << phn_num << "," << email << "," << address << "," << DOB << "," ;
            file.close();
        }
    }
    void update_account_in_file() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        bool found = false;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = true;
                row[7] = to_string(deposit);
                row[8] = to_string(withdrawal);
                row[9] = to_string(amount);
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
    void update_account_deposit() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        int found = 0;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = 1;
                row[7] = to_string(deposit);
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
    void update_account_withdrawal() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        bool found = false;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = true;
                row[8] = to_string(withdrawal);
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
void update_account_Check_bal() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        bool found = false;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = true;
                cout<<"The balance is  : "<< row[9];
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
    void show_account_deposit() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        int found = 0;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = 1;
                cout<<" DEPOSIT AMOUNT : "<<row[7];
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
void show_account_withdrawal() {
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        int found = 0;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = 1;
                cout<<" WITHDRAWAL AMOUNT : "<<row[8];
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
void show_account_deposit_public(){
        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;
        int found = 0;

        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }

            if (row.size() > 0 && stoll(row[1]) == acc_num) {
                found = 1;
                cout<<" BALANCE : "<<row[9];
            }

            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
    void set_pin(){
        long long int search_acc;
        cout << "Enter your account number: ";
        cin >> search_acc;
        if (acc_num == search_acc) {
            cout << "Hi " << name << endl;
            cout << "Enter the ATM PIN: ";
            cin >> atm_pin;
            cout << "Enter the amount to deposit: ";
            cin >> deposit;
            amount += deposit;
            update_account_deposit();
        } else {
            cout << "Invalid Account number!!!" << endl;
        }
    }

void ATM_Pin_search() {
        int atmm;
        cout << "Enter the ATM pin to search: ";
        cin >> atmm;
        if (atm_pin == atmm) {
            int aa;
            cout << "1. Deposit" << endl;
            cout << "2. Withdrawal" << endl;
            cout << "3. Check Balance" << endl;
            cout << "Enter the option: ";
            cin >> aa;
            switch (aa) {
            case 1: {
                cout << "*************Deposit**************" << endl << endl;
                cout << "Enter the amount to deposit: ";
                cin >> deposit;
                amount += deposit;
                update_account_deposit();
                cout << "You have successfully deposited the amount " << deposit << endl;
                cout << "Your current balance is: " << amount << endl;
                break;
            }
            case 2: {
                cout << "*************Withdrawal**************" << endl << endl;
                cout << "Enter the amount to withdraw: ";
                cin >> withdrawal;
                if (withdrawal > amount) {
                    cout << "Insufficient funds" << endl;
                } else {
                    amount -= withdrawal;
                    cout << "You entered withdrawal amount: " << withdrawal << endl << "Now your current balance: " << amount << endl;
                    update_account_withdrawal();
                }
                break;
            }
            case 3: {
                cout << "************Check Balance***************" << endl << endl;
                cout << "Your current balance is: " << amount << endl;
                update_account_Check_bal();
                break;
            }
            default:
                cout << "Invalid option!!!!!" << endl;
            }
        } else {
            cout << "You have entered Wrong Pin number, Try again!!!" << endl;
        }
}
void deposit_public(){
                cout << "*************Deposit**************" << endl << endl;
                cout << "Enter the amount to deposit: ";
                cin >> deposit;
                amount += deposit;
                cout << "You have successfully deposited the amount " << deposit << endl;
                cout << "Your current balance is: " << amount << endl;
                update_account_deposit();
}
void Withdrawal_public(){
                cout << "*************Withdrawal**************" << endl << endl;
                cout << "Enter the amount to withdraw: ";
                cin >> withdrawal;
                if (withdrawal > amount) {
                    cout << "Insufficient funds" << endl;
                } else {
                    amount -= withdrawal;
                    cout << "You entered withdrawal amount: " << withdrawal << endl << "Now your current balance: " << amount << endl;
                    update_account_withdrawal();
                }
}
void check_bal_public(){
                cout << "************Check Balance***************" << endl << endl;
                //cout << "Your current balance is: " << amount << endl;
                update_account_Check_bal();
            }
void Account_number_search() {
        long long int acc_num_search;
        cout << "Enter the Account number to search: ";
        cin >> acc_num_search;
        if (acc_num_search == acc_num) {
            int aa;
            cout << "1. Deposit" << endl;
            cout << "2. Withdrawal" << endl;
            cout << "3. Check Balance" << endl;
            cout << "Enter the option: ";
            cin >> aa;
            switch (aa) {
            case 1: {
                cout << "*************Deposit**************" << endl << endl;
                cout << "Enter the amount to deposit: ";
                cin >> deposit;
                amount += deposit;
                cout << "You have successfully deposited the amount " << deposit << endl;
                cout << "Your current balance is: " << amount << endl;
                update_account_deposit();
                break;
            }
            case 2: {
                cout << "*************Withdrawal**************" << endl << endl;
                cout << "Enter the amount to withdraw: ";
                cin >> withdrawal;
                if (withdrawal > amount) {
                    cout << "Insufficient funds" << endl;
                } else {
                    amount -= withdrawal;
                    cout << "You entered withdrawal amount: " << withdrawal << endl << "Now your current balance: " << amount << endl;
                    update_account_withdrawal();
                }
                break;
            }
            case 3: {
                cout << "************Check Balance***************" << endl << endl;
                cout << "Your current balance is: " << amount << endl;
                update_account_Check_bal();
                break;
            }
            default:
                cout << "Invalid option!!!!!" << endl;
            }
        } else {
            cout << "You have entered Wrong Account number, Try again!!!" << endl;
        }
    }

void atm_working() {
        int op;
        cout << "After creation of account, you can deposit amount via (ATM pin or Account number)" << endl;
        cout << "1. ATM PIN" << endl;
        cout << "2. Account number" << endl;
        cout << "Enter your option: ";
        cin >> op;
        switch (op) {
        case 1:
            ATM_Pin_search();
            break;
        case 2:
            Account_number_search();
            break;
        default:
            cout << "Invalid Option!!!" << endl;
        }
    }

};

class employee : public Account {
public:
    string user_name = "Yashwanth123";
    string password = "Yashwanth@237";

    void check() {
        string username;
        string password1;

        cout << "Enter the username of the employee: ";
        cin >> username;
        if (user_name == username) {
            cout << "Enter the Password: ";
            cin >> password1;
        } else {
            cout << "Invalid username!!!!" << endl;
        }
        if ((user_name == username) && (password == password1)) {
            cout << "1. Create an account" << endl;
            cout << "2. Edit details of an account" << endl;
            cout << "3. ATM working" << endl;
            cout << "Enter the option: ";
            int aa;
            cin >> aa;
            switch (aa) {
            case 1:
                create_acc();
                save_file_create_acc();
                break;
            case 2:
                edit_account();
                break;
            case 3:
                atm_working();
                break;
            default:
                cout << "Invalid option!!!" << endl;
            }
        } else {
            cout << "Invalid password!!!!" << endl;
        }
    }

void edit_account() {
        long long int acc_num_search;
        cout << "Enter the Account number to edit: ";
        cin >> acc_num_search;

        ifstream file("Accounts_public.csv");
        ofstream temp("temp.csv");
        string line, field;
        vector<string> row;

        bool found = false;
        while (getline(file, line)) {
            row.clear();
            stringstream s(line);
            while (getline(s, field, ',')) {
                row.push_back(field);
            }
            if (row.size() > 0 && stoll(row[1]) == acc_num_search) {
                found = true;
                cout << "Editing account for: " << row[0] << endl;
                cout << "Enter new Phone number: ";
                cin >> row[2];
                cout << "Enter new email: ";
                cin >> row[3];
                cout << "Enter new address: ";
                cin >> row[4];
                cout << "Enter new DOB: ";
                cin >> row[5];
                cout << "Account details updated successfully!" << endl;
            }
            for (size_t i = 0; i < row.size(); ++i) {
                temp << row[i];
                if (i < row.size() - 1) temp << ",";
            }
            temp << endl;
        }

        if (!found) {
            cout << "Account number not found!" << endl;
        }

        file.close();
        temp.close();
        remove("Accounts_public.csv");
        rename("temp.csv", "Accounts_public.csv");
    }
};


int main(){
    Account a;
    employee e;
    main11:
    cout<<"\t\t\t\t WELCOME TO ******** BANK "<<endl;
    cout<<"\t\t\t 1. Online Work " <<endl<<endl;
    cout<<"\t\t\t 2. Employee  " <<endl<<endl;
    int opt_main;
    cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
    cin>>opt_main;
    switch(opt_main){
    case 1:{
         cout<<"\t\t\t\t-------------- YOU HAVE SELECTED ONLINE PLATFROM -------------------"<<endl<<endl;
         cout<<"\t\t\t\t ************* IN THIS PLATFROM ******************"<<endl;
         cout<<"\t\t 1 => YOU ARE ABLE TO CREATE AN ACCOUNT\n"<<endl<<endl;
         cout<<"\t\t 2 => YOU ARE ABLE TO SET AN ATM PIN FOR YOUR ACCOUNT"<<endl<<endl;
         cout<<"\t\t 3 => YOU CAN ABLE TO DEPOSIT,WITHDRAWAL,CHECK BALANCE IN YOUR ACCOUNT"<<endl<<endl;
         int opt_main_1;
         cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
         cin>>opt_main_1;
         switch(opt_main_1){
         case 1:
            {
                cout<<"\t\t\t\t----------------- YOU HAVE SELECTED CREATION OF AN ACCOUNT -------------------"<<endl<<endl;
                a.create_acc();
                a.show_acc();
                a.save_file_create_acc();
            }
            break;
         case 2:
            {
                cout<<"\t\t\t\t-------------- YOU HAVE SELECTED SET AN ATM PIN FOR YOUR ACCOUNT -------------------"<<endl<<endl;
                a.set_pin();
            }
            break;
         case 3:
            {
                case3:
                cout<<"\t\t\t\t--------------  YOU HAVE SELECTED DEPOSIT,WITHDRAWAL,CHECK BALANCE IN YOUR ACCOUNT   -------------------"<<endl<<endl;
                cout<<"\t\t\t\t ************* IN THIS PLATFROM ******************"<<endl;
                cout<<"\t\t 1 => DEPOSIT AMOUNT "<<endl<<endl;
                cout<<"\t\t 2 => WITHDRAWAL AMOUNT"<<endl<<endl;
                cout<<"\t\t 3 => CHECK BALANCE"<<endl<<endl;
                cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
                int opt_main_3;
                cin>>opt_main_3;
                    switch(opt_main_3){
               case 1:
                a.update_account_deposit();
                break;
               case 2:
                a.update_account_withdrawal();
                break;
               case 3:
                a.update_account_Check_bal();
                break;
               default:
                cout<<"Invalid option !!,Try again....."<<endl;
                goto case3;
                }
            }
            break;
         }
        }
        break;
    case 2:{
        epl:
         cout<<"\t\t\t\t-------------- YOU HAVE SELECTED EMPLOYEE PLATFROM -------------------"<<endl<<endl;
         cout<<"\t\t\t\t ************* IN THIS PLATFROM ******************"<<endl;
         cout<<"\t\t 1 => CREATE AN ACCOUNT FOR PUBLIC\n"<<endl<<endl;
         cout<<"\t\t 2 => CREATE AN ACCOUNT FOR EMPLOYEES\n"<<endl<<endl;
         cout<<"\t\t 3 => SET AN ATM PIN FOR PUBLIC"<<endl<<endl;
         cout<<"\t\t 4 => SET AN ATM PIN FOR EMPLOYEES"<<endl<<endl;
         cout<<"\t\t 5 => YOU CAN ABLE TO DEPOSIT,WITHDRAWAL,CHECK BALANCE FOR PUBLIC ACCOUNT "<<endl<<endl;
         cout<<"\t\t 6 => YOU CAN ABLE TO DEPOSIT,WITHDRAWAL,CHECK BALANCE FOR EMPLOYEES ACCOUNT"<<endl<<endl;
         int opt_main_2;
         cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
         cin>>opt_main_2;
         switch(opt_main_2)
         {
                case 1:{
                    cout<<endl<<endl;
                    cout<<"\t\t\t\t-------------- YOU HAVE SELECTED CREATE AN ACCOUNT FOR PUBLIC  -------------------"<<endl;
                    a.create_acc();
                    a.show_acc();
                    a.save_file_create_acc();
                       }
                    break;
                case 2:{
                    cout<<endl<<endl;
                    cout<<"\t\t\t\t-------------- YOU HAVE SELECTEDCREATE AN ACCOUNT FOR EMPLOYEES  -------------------"<<endl;
                    e.create_acc();
                    e.show_acc();
                    e.save_file_create_acc();
                       }
                    break;
                case 3:
                       {
                    cout<<"\t\t\t\t-------------- YOU HAVE SELECTED SET AN ATM PIN FOR PUBLIC ACCOUNT -------------------"<<endl;
                    a.set_pin();
                       }
                    break;
                case 4:
                       {
                    cout<<"\t\t\t\t-------------- YOU HAVE SELECTED SET AN ATM PIN FOR EMPLOYEE ACCOUNT -------------------"<<endl;
                    e.set_pin();
                       }
                    break;
                case 5:
                        {
                    case5:
                    cout<<"\t\t\t\t--------------  YOU HAVE SELECTED DEPOSIT,WITHDRAWAL,CHECK BALANCE FOR PUBLIC ACCOUNT   -------------------"<<endl;
                    cout<<"\t\t\t\t ************* IN THIS PLATFROM ******************"<<endl;
                    cout<<"\t\t 1 => DEPOSIT AMOUNT "<<endl;
                    cout<<"\t\t 2 => WITHDRAWAL AMOUNT"<<endl;
                    cout<<"\t\t 3 => CHECK BALANCE"<<endl;
                    cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
                    int opt_main_CASE_4;
                    cin>>opt_main_CASE_4;
                    switch(opt_main_CASE_4){
                        case 1:
                            a.deposit_public();
                            break;
                        case 2:
                            a.Withdrawal_public();
                            break;
                        case 3:
                            a.check_bal_public();
                            break;
                        default:
                            cout<<"Invalid option !!,Try again....."<<endl;
                            goto case5;
                            }
                        }
                        break;
            case 6:
                    {
                        case6:
                        cout<<"\t\t\t\t--------------  YOU HAVE SELECTED DEPOSIT,WITHDRAWAL,CHECK BALANCE FOR EMPLOYEES ACCOUNT   -------------------"<<endl<<endl;
                        cout<<"\t\t\t\t ************* IN THIS PLATFROM ******************"<<endl;
                        cout<<"\t\t 1 => DEPOSIT AMOUNT "<<endl<<endl;
                        cout<<"\t\t 2 => WITHDRAWAL AMOUNT"<<endl<<endl;
                        cout<<"\t\t 3 => CHECK BALANCE"<<endl<<endl;
                        cout<<"\t\t\t SELECT THE OPTION FROM THE ABOVE OPTIONS : ";
                        int opt_main_CASE_5;
                        cin>>opt_main_CASE_5;
                        switch(opt_main_CASE_5){
                        case 1:
                        e.deposit_public();
                        break;
                        case 2:
                        e.Withdrawal_public();
                        break;
                        case 3:
                        e.check_bal_public();
                        break;
                        default:
                        cout<<"Invalid option !!,Try again....."<<endl;
                        goto case5;
                    }
                        break;
                }
                break;
            default:
                 cout<<"Invalid option !!!,Try Again....... "<<endl;
                 goto epl;
         }
    }
     break;
default:
    cout<<"Invalid option !!!,Try Again....... "<<endl;
    goto main11;
    }
}
