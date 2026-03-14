import json
import os

DB_FILE = "library.json"

def load_books():
    if os.path.exists(DB_FILE):
        with open(DB_FILE, "r", encoding="utf-8") as f:
            return json.load(f)
    return []

def save_books(books):
    with open(DB_FILE, "w", encoding="utf-8") as f:
        json.dump(books, f, ensure_ascii=False, indent=4)

def main():
    books = load_books()

    while True:
        print("\n--- Т-БИБЛИОТЕКА ---")
        print("1. Добавить книгу")
        print("2. Показать все книги")
        print("3. Найти книгу")
        print("4. Поменять статус (прочитано)")
        print("5. В избранное / Из избранного")
        print("6. Рекомендации и избранное")
        print("7. Удалить книгу")
        print("0. Выход")

        vibor = input("\nЧто сделать? ")

        if vibor == "1":
            print("\nВведите данные новой книги:")
            nazvanie = input("Название: ")
            avtor = input("Автор: ")
            janr = input("Жанр: ")
            god = input("Год: ")
            opisanie = input("Описание: ")

            new_book = {
                "id": len(books) + 1,
                "title": nazvanie,
                "author": avtor,
                "genre": janr,
                "year": god,
                "desc": opisanie,
                "is_read": False,
                "is_fav": False
            }
            books.append(new_book)
            save_books(books)
            print("Готово! Книга добавлена.")

        elif vibor == "2":
            if not books:
                print("В библиотеке пока пусто.")
            else:
                print("\nСписок всех книг:")
                print("Сортировать по: 1 - Названию, 2 - Году, 3 - Без сортировки")
                s_vibor = input("Выбор: ")
                
                spisok_dlya_vivoda = books.copy()
                if s_vibor == "1":
                    spisok_dlya_vivoda.sort(key=lambda x: x["title"].lower())
                elif s_vibor == "2":
                    spisok_dlya_vivoda.sort(key=lambda x: x["year"])

                for b in spisok_dlya_vivoda:
                    read_str = "[Прочитано]" if b["is_read"] else "[Не читал]"
                    fav_str = "⭐" if b["is_fav"] else ""
                    print(f"ID: {b['id']} | {b['title']} - {b['author']} ({b['year']}) {read_str} {fav_str}")

        elif vibor == "3":
            poisk = input("\nЧто ищем (название или автор)? ").lower()
            found = False
            for b in books:
                if poisk in b["title"].lower() or poisk in b["author"].lower():
                    print(f"Найдено: {b['title']} (ID: {b['id']})")
                    found = True
            if not found:
                print("Ничего не нашли.")

        elif vibor == "4":
            b_id = input("\nВведите ID книги, чтобы отметить как прочитанную: ")
            for b in books:
                if str(b["id"]) == b_id:
                    b["is_read"] = not b["is_read"]
                    save_books(books)
                    print(f"Статус книги '{b['title']}' изменен!")
                    break

        elif vibor == "5":
            b_id = input("\nВведите ID книги для избранного: ")
            for b in books:
                if str(b["id"]) == b_id:
                    b["is_fav"] = not b["is_fav"]
                    save_books(books)
                    print("Статус избранного изменен!")
                    break

        elif vibor == "6":
            print("\n--- Избранные книги ---")
            for b in books:
                if b["is_fav"]:
                    print(f"- {b['title']}")
            
            print("\n--- Можно почитать (тот же жанр) ---")
            my_genres = []
            for b in books:
                if b["is_read"]:
                    my_genres.append(b["genre"])
            
            for b in books:
                if not b["is_read"] and b["genre"] in my_genres:
                    print(f"Рекомендуем: {b['title']} (потому что вам нравится {b['genre']})")

        elif vibor == "7":
            b_id = input("\nВведите ID книги для удаления: ")
            for b in books:
                if str(b["id"]) == b_id:
                    books.remove(b)
                    save_books(books)
                    print("Книга удалена!")
                    break

        elif vibor == "0":
            print("Пока!")
            break
        else:
            print("Нет такого пункта.")

if __name__ == "__main__":
    main()


