# Social-Network-by-Zangar

from tkinter import *
from tkinter import messagebox
import pickle

root = Tk()
root.geometry("300x500")
root.title('Войти в систему')


def registration():
    text = Label(text="Для входа в систему зарегистрируйтесь !")
    text_login = Label(text="Введите логин : ")
    registr_login = Entry()
    text_password1 = Label(text="Введите пароль : ")
    registr_password1 = Entry()
    text_password2 = Label(text="Повторите пароль : ")
    registr_password2 = Entry(show="*")
    button_registr = Button(text="Зарегистрироваться", command=lambda: save())
    text.pack()
    text_login.pack()
    registr_login.pack()
    text_password1.pack()
    registr_password1.pack()
    text_password2.pack()
    registr_password2.pack()
    button_registr.pack()

    def save():
        login_pass_save = {}
        login_pass_save[registr_login.get()] = registr_password1.get()
        f = open('login_pass.txt', 'wb')
        pickle.dump(login_pass_save, f)
        f.close()
        login()


def login():
    text_log = Label(text="Поздравляем!")
    text_enter_login = Label(text="Введите логин : ")
    enter_login = Entry()
    text_enter_pass = Label(text="Введите пароль : ")
    enter_password = Entry(show="*")
    text_log.pack()
    button_login = Button(text="Войти", command=lambda: log_pass())
    text_enter_login.pack()
    enter_login.pack()
    text_enter_pass.pack()
    enter_password.pack()
    button_login.pack()

    def log_pass():
        f = open('login_pass.txt', 'rb')
        a = pickle.load(f)
        f.close()
        if enter_login.get() in a:
            if enter_password.get() == a[enter_login.get()]:
                messagebox.showinfo("Вход выполнен.", "Привет! У тебя 5 новых сообщений.")
            else:
                messagebox.showerror("Ошибка!", "Вы вели неверный логин или пароль. ")
        else:
            messagebox.showerror("Ошибка!", "Неверный логин.")


registration()
root.mainloop()
