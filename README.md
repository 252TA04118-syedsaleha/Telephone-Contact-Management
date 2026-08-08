#include <stdio.h>
#include <string.h>

#define MAX_CONTACTS 100

struct Contact {
    int id;
    char name[50];
    char phone[20];
    char email[60];
    char address[100];
    char category[30];
    int callCount;
};

struct Contact contacts[MAX_CONTACTS];
int contactCount = 0;


/* Add a new contact */
void addContact() {

    if (contactCount >= MAX_CONTACTS) {
        printf("\nContact storage is full!\n");
        return;
    }

    printf("\n========== ADD CONTACT ==========\n");

    printf("Enter Contact ID: ");
    scanf("%d", &contacts[contactCount].id);

    printf("Enter Name: ");
    scanf(" %[^\n]", contacts[contactCount].name);

    printf("Enter Phone Number: ");
    scanf("%s", contacts[contactCount].phone);

    printf("Enter Email: ");
    scanf("%s", contacts[contactCount].email);

    printf("Enter Address: ");
    scanf(" %[^\n]", contacts[contactCount].address);

    printf("Enter Category: ");
    scanf(" %[^\n]", contacts[contactCount].category);

    contacts[contactCount].callCount = 0;

    contactCount++;

    printf("\nContact added successfully!\n");
}


/* Display one contact */
void displayContact(struct Contact c) {

    printf("\n------------------------------------------\n");
    printf("Contact ID : %d\n", c.id);
    printf("Name       : %s\n", c.name);
    printf("Phone      : %s\n", c.phone);
    printf("Email      : %s\n", c.email);
    printf("Address    : %s\n", c.address);
    printf("Category   : %s\n", c.category);
    printf("Call Count : %d\n", c.callCount);
}


/* Display all contacts */
void displayContacts() {

    int i;

    if (contactCount == 0) {
        printf("\nNo contacts available.\n");
        return;
    }

    printf("\n========== TELEPHONE CONTACTS ==========\n");

    for (i = 0; i < contactCount; i++) {
        displayContact(contacts[i]);
    }
}


/* Search contact by ID */
void searchByID() {

    int id;
    int i;
    int found = 0;

    printf("\nEnter Contact ID: ");
    scanf("%d", &id);

    for (i = 0; i < contactCount; i++) {

        if (contacts[i].id == id) {

            printf("\n========== CONTACT FOUND ==========\n");
            displayContact(contacts[i]);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nContact not found!\n");
    }
}


/* Search contact by name */
void searchByName() {

    char name[50];
    int i;
    int found = 0;

    printf("\nEnter Name: ");
    scanf(" %[^\n]", name);

    printf("\n========== NAME SEARCH ==========\n");

    for (i = 0; i < contactCount; i++) {

        if (strcmp(contacts[i].name, name) == 0) {

            displayContact(contacts[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo contact found with this name.\n");
    }
}


/* Search contact by category */
void searchByCategory() {

    char category[30];
    int i;
    int found = 0;

    printf("\nEnter Category: ");
    scanf(" %[^\n]", category);

    printf("\n========== CATEGORY SEARCH ==========\n");

    for (i = 0; i < contactCount; i++) {

        if (strcmp(contacts[i].category, category) == 0) {

            displayContact(contacts[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo contacts found in this category.\n");
    }
}


/* Search phone number */
void searchByPhone() {

    char phone[20];
    int i;
    int found = 0;

    printf("\nEnter Phone Number: ");
    scanf("%s", phone);

    for (i = 0; i < contactCount; i++) {

        if (strcmp(contacts[i].phone, phone) == 0) {

            printf("\n========== PHONE NUMBER FOUND ==========\n");
            displayContact(contacts[i]);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nPhone number not found!\n");
    }
}


/* Make a telephone call */
void makeCall() {

    int id;
    int i;
    int found = 0;

    printf("\nEnter Contact ID to call: ");
    scanf("%d", &id);

    for (i = 0; i < contactCount; i++) {

        if (contacts[i].id == id) {

            found = 1;

            contacts[i].callCount++;

            printf("\nCalling %s...\n", contacts[i].name);
            printf("Phone Number: %s\n", contacts[i].phone);
            printf("Call connected successfully!\n");

            break;
        }
    }

    if (!found) {
        printf("\nContact not found!\n");
    }
}


/* Update contact */
void updateContact() {

    int id;
    int i;
    int found = 0;

    printf("\nEnter Contact ID to update: ");
    scanf("%d", &id);

    for (i = 0; i < contactCount; i++) {

        if (contacts[i].id == id) {

            found = 1;

            printf("\n========== UPDATE CONTACT ==========\n");

            printf("Enter New Name: ");
            scanf(" %[^\n]", contacts[i].name);

            printf("Enter New Phone Number: ");
            scanf("%s", contacts[i].phone);

            printf("Enter New Email: ");
            scanf("%s", contacts[i].email);

            printf("Enter New Address: ");
            scanf(" %[^\n]", contacts[i].address);

            printf("Enter New Category: ");
            scanf(" %[^\n]", contacts[i].category);

            printf("\nContact updated successfully!\n");

            break;
        }
    }

    if (!found) {
        printf("\nContact not found!\n");
    }
}


/* Delete contact */
void deleteContact() {

    int id;
    int i, j;
    int found = 0;

    printf("\nEnter Contact ID to delete: ");
    scanf("%d", &id);

    for (i = 0; i < contactCount; i++) {

        if (contacts[i].id == id) {

            found = 1;

            for (j = i; j < contactCount - 1; j++) {
                contacts[j] = contacts[j + 1];
            }

            contactCount--;

            printf("\nContact deleted successfully!\n");

            break;
        }
    }

    if (!found) {
        printf("\nContact not found!\n");
    }
}


/* Display call history */
void callReport() {

    int i;

    printf("\n========== CALL REPORT ==========\n");

    if (contactCount == 0) {
        printf("No contacts available.\n");
        return;
    }

    for (i = 0; i < contactCount; i++) {

        printf("\nName       : %s", contacts[i].name);
        printf("\nPhone      : %s", contacts[i].phone);
        printf("\nCall Count : %d\n", contacts[i].callCount);
    }
}


/* Main function */
int main() {

    int choice;

    printf("================================================\n");
    printf("          TELEPHONE MANAGEMENT SYSTEM\n");
    printf("================================================\n");

    do {

        printf("\n================ MAIN MENU ================\n");
        printf("1.  Add Contact\n");
        printf("2.  Display All Contacts\n");
        printf("3.  Search by ID\n");
        printf("4.  Search by Name\n");
        printf("5.  Search by Category\n");
        printf("6.  Search by Phone Number\n");
        printf("7.  Make a Call\n");
        printf("8.  Update Contact\n");
        printf("9.  Delete Contact\n");
        printf("10. Call Report\n");
        printf("11. Exit\n");
        printf("============================================\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {

            case 1:
                addContact();
                break;

            case 2:
                displayContacts();
                break;

            case 3:
                searchByID();
                break;

            case 4:
                searchByName();
                break;

            case 5:
                searchByCategory();
                break;

            case 6:
                searchByPhone();
                break;

            case 7:
                makeCall();
                break;

            case 8:
                updateContact();
                break;

            case 9:
                deleteContact();
                break;

            case 10:
                callReport();
                break;

            case 11:
                printf("\nThank you for using Telephone Management System!\n");
                break;

            default:
                printf("\nInvalid choice! Please try again.\n");
        }

    } while (choice != 11);

    return 0;
}
