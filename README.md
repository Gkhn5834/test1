import os

def create_notepad():
    try:
        file_name = input("Enter the name of the notepad: ")
        with open(file_name, 'w') as file:
            print("Notepad created:", file_name)
    except Exception as e:
        print("Error occurred:", e)

def write_to_notepad():
    try:
        file_name = input("Enter the name of the notepad: ")
        with open(file_name, 'a') as file:
            while True:
                note_content = input("Enter the text you want to write in the notepad (type 'exit' to quit): ")
                if note_content.lower() == 'exit':
                    break
                file.write(note_content + '\n')
        print("Successfully written to the notepad.")
    except Exception as e:
        print("Error occurred:", e)

import os

def search_notepad():
    try:
        search_text = input("Enter the text you want to search for: ").lower()

        # List all .txt files in the current directory
        txt_files = [file for file in os.listdir() if file.endswith(".txt")]

        if not txt_files:
            print("No notepad files (.txt) found in the current directory.")
            return

        matching_files = [file for file in txt_files if search_text in file.lower()]

        if matching_files:
            print(f"Matching files: {', '.join(matching_files)}")
            selected_file = input("Enter the exact name of the notepad you want to view (without .txt): ").lower()
            if selected_file + '.txt' in [file.lower() for file in matching_files]:
                with open(selected_file + '.txt', 'r') as file:
                    lines = file.readlines()
                    print(f"\nText found in notepad ({selected_file}.txt):")
                    for line in lines:
                        print(line.strip())
            else:
                print("Invalid file name. The file does not exist.")
        else:
            print("No file matches the search text.")
        
    except Exception as e:
        print("Error occurred:", e)


def view_notepad():
    try:
        print("\nAvailable notepad files:")
        file_list = [f for f in os.listdir('.') if os.path.isfile(f) and f.endswith('.txt')]
        for idx, file in enumerate(file_list, start=1):
            print(f"{idx}. {file}")
        
        choice = int(input("Enter the number of the notepad you want to view (0 to cancel): "))
        if choice == 0:
            return
        
        selected_file = file_list[choice - 1]
        with open(selected_file, 'r') as file:
            print(f"\nContents of {selected_file}:")
            for line in file:
                print(line.strip())
        
        delete_option = input(f"Do you want to delete {selected_file}? (Y/N): ")
        if delete_option.lower() == 'y':
            os.remove(selected_file)
            print(f"{selected_file} has been deleted.")
    except Exception as e:
        print("Error occurred:", e)
def update_notepad():
    try:
        print("\nAvailable notepad files:")
        file_list = [f for f in os.listdir('.') if os.path.isfile(f) and f.endswith('.txt')]
        for idx, file in enumerate(file_list, start=1):
            print(f"{idx}. {file}")
        
        choice = int(input("Enter the number of the notepad you want to update (0 to cancel): "))
        if choice == 0:
            return
        
        selected_file = file_list[choice - 1]
        if not selected_file.endswith('.txt'):
            selected_file += '.txt'

        with open(selected_file, 'a') as file:
            while True:
                note_content = input("Enter the text you want to add to the notepad (type 'exit' to quit): ")
                if note_content.lower() == 'exit':
                    break
                file.write(note_content + '\n')
        print("Successfully updated the notepad.")
    except Exception as e:
        print("Error occurred:", e)

def delete_notepad():
    try:
        print("\nAvailable notepad files:")
        file_list = [f for f in os.listdir('.') if os.path.isfile(f) and f.endswith('.txt')]
        for idx, file in enumerate(file_list, start=1):
            print(f"{idx}. {file}")

        choice = int(input("Enter the number of the notepad you want to delete (0 to cancel): "))
        if choice == 0:
            return

        selected_file = file_list[choice - 1]
        os.remove(selected_file)
        print(f"{selected_file} has been deleted.")

    except Exception as e:
        print("Error occurred:", e)

def main_menu():
    while True:
        print("\nMain Menu")
        print("1. Create Notepad")
        print("2. Write to Notepad")
        print("3. Search Notepad")
        print("4. View Notepad")
        print("5. Update Notepad")
        print("6. Delete Notepad")  # Silme seçeneğini ekledik
        print("7. Exit")  # Çıkış seçeneği numarasını güncelledik

        choice = input("Enter your choice (1/2/3/4/5/6/7/8): ")

        if choice == '1':
            create_notepad()
        elif choice == '2':
            write_to_notepad()
        elif choice == '3':
            search_notepad()
        elif choice == '4':
            view_notepad()
        elif choice == '5':
            update_notepad()
        elif choice == '6':
            delete_notepad()  # Silme işlemini buradan çağırıyoruz
        elif choice == '7':
            print("Exiting the program...")
            break
        else:
            print("Invalid choice, please try again.")

if __name__ == "__main__":
    main_menu()
