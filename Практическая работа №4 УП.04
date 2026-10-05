
import tkinter as tk  
from tkinter import messagebox  
import hashlib  



def hash_password(password: str) -> str:
    """Превращает пароль в хеш SHA-256."""
    return hashlib.sha256(password.encode()).hexdigest()


USERS = {
    "admin": hash_password("1234"),
    "user": hash_password("qwerty"),
}


MAX_ATTEMPTS = 3
attempts_left = MAX_ATTEMPTS



def toggle_password_visibility():
    """Показывает/скрывает пароль по нажатию на чекбокс."""
    if show_password_var.get():
        
        entry_password.config(show="")
    else:
       
        entry_password.config(show="*")


def check_login(event=None):
    """
    Проверяет введённые логин и пароль.
    event=None нужен, чтобы функцию можно было вызывать
    и по кнопке, и по нажатию Enter.
    """
    global attempts_left  

   
    login = entry_login.get().strip()  # .strip() убирает пробелы по краям
    password = entry_password.get()

    if not login or not password:
        messagebox.showwarning("Внимание", "Заполните все поля!")
        return  

    
    password_hash = hash_password(password)

    if login in USERS and USERS[login] == password_hash:
        messagebox.showinfo("Успех", f"Добро пожаловать, {login}!")
        # Здесь обычно открывают главное окно приложения:
        # root.destroy()
        # open_main_window()
        return
    else:
        # Неверные данные
        attempts_left -= 1  # Уменьшаем счётчик попыток
        if attempts_left > 0:
            messagebox.showerror(
                "Ошибка",
                f"Неверный логин или пароль.\n"
                f"Осталось попыток: {attempts_left}"
            )
        else:
            messagebox.showerror(
                "Блокировка",
                "Превышено число попыток. Приложение будет закрыто."
            )
            root.destroy()  # Закрываем окно
            return

        # Очищаем поле пароля и ставим туда курсор
        entry_password.delete(0, tk.END)
        entry_password.focus()


# СОЗДАНИЕ ГЛАВНОГО ОКНА
root = tk.Tk()  # Создаём окно
root.title("Авторизация")  # Заголовок окна
root.geometry("360x320")  # Размер: ширина х высота
root.resizable(False, False)  # Запрещаем менять размер

label_title = tk.Label(
    root,
    text="Вход в систему",
    font=("Arial", 16, "bold")  # Шрифт: Arial 16, жирный
)
label_title.pack(pady=15)  # pady – отступ сверху и снизу

label_login = tk.Label(root, text="Логин:")
label_login.pack(anchor="w", padx=40)  # anchor="w" – прижать влево

entry_login = tk.Entry(root, width=30)  # Поле ввода шириной 30 символов
entry_login.pack(padx=40, pady=5)
entry_login.focus()  # Курсор сразу в этом поле


label_password = tk.Label(root, text="Пароль:")
label_password.pack(anchor="w", padx=40)

entry_password = tk.Entry(
    root,
    width=30,
    show="*"  # Скрываем символы звёздочками
)
entry_password.pack(padx=40, pady=5)

show_password_var = tk.BooleanVar(value=False)  # Переменная для галочки

check_show = tk.Checkbutton(
    root,
    text="Показать пароль",
    variable=show_password_var,
    command=toggle_password_visibility  # Вызов при клике
)
check_show.pack(anchor="w", padx=40)


btn_login = tk.Button(
    root,
    text="Войти",
    width=15,
    command=check_login,  # Функция, вызываемая при клике
    bg="#4CAF50",  # Цвет фона (зелёный)
    fg="white",  # Цвет текста
    activebackground="#45a049",  # Цвет при нажатии
    cursor="hand2"  # Курсор-рука при наведении
)
btn_login.pack(pady=20)


root.bind("<Return>", check_login)
root.mainloop()
