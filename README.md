# Address Book (command line)

A Python program to manage an address book, built with two classes:
`Contact` (a single record) and `AddressBook` (the collection and the operations on it).
Contacts are saved to `contacts.json` and automatically reloaded at startup.

## Contact data
- **Required:** name, surname and phone number
- **Optional:** email

## Menu
1. **Add** a contact
2. **Show** the full list of contacts
3. **Search** by name or surname, even partially
4. **Edit** a contact's data
5. **Delete** a contact (with confirmation, default "No")
0. **Exit**, saving the data

During add, search, edit and delete you can cancel at any time
by typing `0`, and you go back to the menu.

## How to run it
1. Open the notebook in Google Colab and run all the cells (Runtime → Run all).
2. The demo cell creates sample contacts in `contacts.json` (if the file does not exist yet) and reloads them.
3. In the last cell, use the menu.

## Things to try
- Show the list (choice 2).
- Search for "Yagami": it finds several contacts sharing a surname (choice 3).
- Add your own contact, leaving the email empty (choice 1).
- Edit a phone number: press enter to keep a field unchanged (choice 4).
- Delete a contact and notice the confirmation prompt (choice 5).
- Try invalid input: a phone number with letters, an email without `@`, a number outside the list.
- Exit with `0`, run the last cell again and check that the data is still there.

## Design choices
**Data structure:** a list of `Contact` objects. The search is partial (any part of the name or surname), so every contact has to be checked anyway, and a dictionary would bring no advantage. A list also keeps the methods simple to write and verify. Edit and delete scan the list, which is acceptable for a prototype; if the address book grew very large, a dictionary of lists (key = lowercase full name) would be a natural evolution.

**Persistence:** JSON cannot store `Contact` objects, so `to_dict()` turns each contact into a dictionary before saving, and `load()` rebuilds the objects from the file. A missing, empty or corrupted file does not stop the program: the address book simply starts empty, and incomplete records are skipped.

**Known limitation:** the program does not prevent two contacts with the same full name. Since edit and delete work on the contact chosen from a numbered list, they still act on the right one.

**Language convention:** code, comments and on-screen messages are all in English.
