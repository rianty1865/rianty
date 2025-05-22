class Node:
    def __init__(self, nama, pesan):
        self.nama = nama
        self.pesan = pesan
        self.next = None

class GuestBook:
    def __init__(self, filename="guestbook.txt"):
        self.head = None
        self.filename = filename
        self.load_from_file()

    def load_from_file(self):
        try:
            with open(self.filename, "r") as f:
                lines = f.readlines()
                for line in lines:
                    nama, pesan = line.strip().split(";", 1) # Split by semicolon, handle potential multiple semicolons in message
                    self.add_entry(nama, pesan)
        except FileNotFoundError:
            pass  # File doesn't exist yet, start with an empty list

    def save_to_file(self):
        with open(self.filename, "w") as f:
            current = self.head
            while current:
                f.write(f"{current.nama};{current.pesan}\n")
                current = current.next

    def add_entry(self, nama, pesan):
        new_node = Node(nama, pesan)
        new_node.next = self.head
        self.head = new_node
        self.save_to_file()
        print("Entry added successfully!")

    def show_entries(self):
        if not self.head:
            print("Guestbook is empty.")
            return

        current = self.head
        print("----- Guestbook Entries -----")
        while current:
            print(f"Nama: {current.nama}, Pesan: {current.pesan}")
            current = current.next
        print("----------------------------")


if __name__ == "__main__":
    guestbook = GuestBook()

    while True:
        print("\nMenu:")
        print("1. Add entry")
        print("2. Show entries")
        print("3. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            nama = input("Enter your name: ")
            pesan = input("Enter your message: ")
            guestbook.add_entry(nama, pesan)
        elif choice == "2":
            guestbook.show_entries()
        elif choice == "3":
            break
        else:
            print("invalid choice.")
            
autput:
Menu:
1. Add entry
2. Show entries
3. Exit

          
