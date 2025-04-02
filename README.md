# 5.1 Класс Автор
class Author:
    def __init__(self, full_name: 'ФИО автора', country: 'Страна происхождения'):
        """Создает автора с ФИО и страной."""
        self.full_name = full_name
        self.country = country

    def display_info(self):
        """Выводит информацию об авторе."""
        print(f"Автор: {self.full_name}, Страна: {self.country}")


# Основная программа
n = int(input("Введите количество авторов: "))
authors = []
for _ in range(n):
    name = input("Введите ФИО автора: ")
    country = input("Введите страну автора: ")
    authors.append(Author(name, country))

print("\nВсе авторы:")
for author in authors:
    author.display_info()

print("\nРусские авторы:")
for author in authors:
    if author.country.lower() == "россия":
        author.display_info()


# 5.2 Класс Книга
class Book:
    def __init__(self, title: 'Название книги'):
        """Создает книгу с заданным названием."""
        self.title = title
        self.__content = []  # Приватное поле для содержания книги
        print(f"Книга '{self.title}' создана")

    def __del__(self):
        """Выводит сообщение при удалении книги."""
        print(f"Книга '{self.title}' удалена")

    # 5.3 Методы для работы с содержанием
    def add_work(self, work: 'Название произведения'):
        """Добавляет произведение в содержание книги."""
        self.__content.append(work)

    def get_work_count(self):
        """Возвращает количество произведений в книге."""
        return len(self.__content)

    # 5.4 Метод вывода информации о книге
    def display_info(self):
        """Выводит информацию о книге и ее содержании."""
        print(f"Книга: {self.title}")
        print("Содержание:")
        for i, work in enumerate(self.__content, 1):
            print(f"{i}) {work}")


# 5.5 Класс Книга Автора (наследует от Author и Book)
class AuthorBook(Author, Book):
    def __init__(self, full_name, country, title):
        """Создает книгу с автором."""
        Author.__init__(self, full_name, country)
        Book.__init__(self, title)

    def display_full_info(self):
        """Выводит ФИО автора, название книги и её содержание."""
        print(f"Автор: {self.full_name}")
        self.display_info()


# Тестирование классов
if __name__ == "__main__":
    # Тестирование класса AuthorBook
    ab = AuthorBook("Александр Пушкин", "Россия", "Сказки")
    ab.add_work("Сказка о царе Салтане")
    ab.add_work("Сказка о рыбаке и рыбке")
    ab.display_full_info()

    del ab
