# kedai_kopi_nanda
class AnandaCoffee:
    def __init__(self):
        self._menu = {
            "a": ("ES Kopi Susu", 11000),
            "b": ("ES Kopi Coklat", 12000),
            "c": ("ES Kopi Hitam", 11000),
            "d": ("Ice Americano", 14000),
        }

    def show_menu(self):
        print(
            """
        ==============================
        Ananda Coffee
        List Menu Minuman Kopi
        ==============================
        A. ES Kopi Susu : Rp 11.000
        B. ES Kopi Coklat : Rp 12.000
        C. ES Kopi Hitam : Rp 11.000
        D. Ice Americano : Rp 14.000
        ==============================
        """
        )

    def calculate_price(self, choice, qty):
        if choice not in self._menu:
            raise ValueError("Menu tidak tersedia")

        name, price = self._menu[choice]
        total_price = price * qty
        discount = Discount.calculate_discount(qty, total_price)
        tax = int(total_price * 0.1)
        total_price = total_price - discount + tax

        return name, price, qty, discount, tax, total_price


class Discount:
    @staticmethod
    def calculate_discount(qty, total_price):
        if qty >= 10:
            discount = int(total_price * 0.25)
        elif qty >= 7:
            discount = int(total_price * 0.2)
        elif qty >= 5:
            discount = int(total_price * 0.15)
        elif qty >= 3:
            discount = int(total_price * 0.1)
        else:
            discount = 0

        return discount


if __name__ == "__main__":
    cafe = AnandaCoffee()

    choice = "y"
    while choice.lower() == "y":
        cafe.show_menu()
        menu_choice = input("Masukkan pilihan menu kopi (a/b/c/d): ")
        qty = int(input("Masukkan jumlah pesanan: "))

        try:
            name, price, qty, discount, tax, total_price = cafe.calculate_price(
                menu_choice, qty
            )
        except ValueError as e:
            print(e)
            choice = input("Apakah Anda ingin melanjutkan? (y/n) ")
            continue

        print("--------------------------")
        print("Ananda Coffee")
        print("--------------------------")
        print(f"Menu: {name}")
        print(f"Jumlah Pesan: {qty}")
        print(f"Harga: {price}")
        print(f"Diskon: {discount}")
        print(f"PPN: {tax}")
        print("--------------------------")
        print(f"Jumlah Bayar: {total_price}")
        print("--------------------------")

        choice = input("Apakah Anda ingin order kembali? (y/n) ")
