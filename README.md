# BLOOD-BANK-MANAGEMENT-SYSTEM
#include <iostream>
#include <string>
#include <unordered_map>
#include <list>
using namespace std;

// Blood Donation details class
class Donor {
public:
    string name;
    string bloodGroup;
    string contact;

    Donor(string name, string bloodGroup, string contact) {
        this->name = name;
        this->bloodGroup = bloodGroup;
        this->contact = contact;
    }
};

// Blood Bank Class to manage Donors, Stock and Requests
class BloodBank {
private:
    // HashMap for Blood Group Stocks (blood type -> number of units)
    unordered_map<string, int> bloodStock;
    // List of Donors (Linked List)
    list<Donor> donors;

public:
    // Register a Donor
    void registerDonor(string name, string bloodGroup, string contact) {
        Donor donor(name, bloodGroup, contact);
        donors.push_back(donor);
        bloodStock[bloodGroup]++;
        cout << "Donor Registered Successfully!" << endl;
    }

    // Display Blood Bank Stock
    void displayStock() {
        cout << "Blood Bank Stock: " << endl;
        for (const auto& stock : bloodStock) {
            cout << "Blood Group: " << stock.first << " | Units: " << stock.second << endl;
        }
    }

    // Request Blood
    void requestBlood(string bloodGroup) {
        if (bloodStock.find(bloodGroup) != bloodStock.end() && bloodStock[bloodGroup] > 0) {
            bloodStock[bloodGroup]--;
            cout << "Blood for group " << bloodGroup << " has been dispensed." << endl;
        } else {
            cout << "Sorry, no available blood for group " << bloodGroup << " at the moment." << endl;
        }
    }

    // Display Donors
    void displayDonors() {
        cout << "Registered Donors: " << endl;
        for (const auto& donor : donors) {
            cout << "Name: " << donor.name << " | Blood Group: " << donor.bloodGroup << " | Contact: " << donor.contact << endl;
        }
    }
};

int main() {
    BloodBank bb;
    int choice;
    string name, bloodGroup, contact;

    do {
        cout << "\nBlood Bank Management System" << endl;
        cout << "1. Register Donor" << endl;
        cout << "2. Display Blood Stock" << endl;
        cout << "3. Request Blood" << endl;
        cout << "4. Display Donors" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                // Register Donor
                cout << "Enter Donor Name: ";
                cin.ignore();  // To clear the input buffer
                getline(cin, name);
                cout << "Enter Blood Group: ";
                cin >> bloodGroup;
                cout << "Enter Contact Information: ";
                cin >> contact;
                bb.registerDonor(name, bloodGroup, contact);
                break;

            case 2:
                // Display Stock
                bb.displayStock();
                break;

            case 3:
                // Request Blood
                cout << "Enter Blood Group for Request: ";
                cin >> bloodGroup;
                bb.requestBlood(bloodGroup);
                break;

            case 4:
                // Display Donors
                bb.displayDonors();
                break;

            case 5:
                // Exit
                cout << "Exiting... Thank you!" << endl;
                break;

            default:
                cout << "Invalid choice, please try again." << endl;
        }
    } while (choice != 5);

    return 0;
}
