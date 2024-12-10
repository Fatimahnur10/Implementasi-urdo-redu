# Implementasi-urdo-redu
class UndoRedo:
    def __init__(self):
        self.undo_stack = []  # Stack untuk undo
        self.redo_stack = []  # Stack untuk redo

    def perform_action(self, action):
        """Melakukan aksi baru dan menambahkan ke undo stack."""
        self.undo_stack.append(action)
        self.redo_stack.clear()  # Menghapus redo karena aksi baru
        print(f"Action performed: {action}")
        self.show_stacks()

    def undo(self):
        """Melakukan undo (membatalkan aksi terakhir)."""
        if not self.undo_stack:
            print("Nothing to undo!")
            return
        action = self.undo_stack.pop()
        self.redo_stack.append(action)
        print(f"Undo performed: {action}")
        self.show_stacks()

    def redo(self):
        """Melakukan redo (mengembalikan aksi yang dibatalkan)."""
        if not self.redo_stack:
            print("Nothing to redo!")
            return
        action = self.redo_stack.pop()
        self.undo_stack.append(action)
        print(f"Redo performed: {action}")
        self.show_stacks()

    def show_stacks(self):
        """Menampilkan isi stack undo dan redo."""
        print(f"Undo stack: {self.undo_stack}")
        print(f"Redo stack: {self.redo_stack}")
        print("-" * 30)


# Contoh Penggunaan
if __name__ == "__main__":
    undo_redo = UndoRedo()

    # Menambahkan aksi
    undo_redo.perform_action("Write 'Hello'")
    undo_redo.perform_action("Write 'World'")
    undo_redo.perform_action("Write 'Python'")

    # Undo dan redo
    undo_redo.undo()  # Membatalkan 'Write Python'
    undo_redo.undo()  # Membatalkan 'Write World'
    undo_redo.redo()  # Mengembalikan 'Write World'
    undo_redo.undo()  # Membatalkan 'Write World' lagi
    undo_redo.redo()  # Mengembalikan 'Write World'
    undo_redo.redo()  # Mengembalikan 'Write Python'
