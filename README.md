# py_5
# 1 и 2
```
documents = [
    {"type": "passport", "number": "2207 876234", "name": "Василий Гупкин"},
    {"type": "invoice", "number": "11-2", "name": "Геннадий Покемонов"},
    {"type": "insurance", "number": "10006", "name": "Аристарх Павлов"}
]
directories = {
    '1': ['2207 876234', '11-2'],
    '2': ['10006'],
    '3': []
}


def get_name_by_id(n):
    res = None
    for i in documents:
        if i["number"] == n:
            res = (i["name"])
    return res


def get_shelf_by_n_doc(n):
    res = None
    for k, v in directories.items():
        if n in v:
            res = k
            break
    return res


def print_doc():
    for i in documents:
        print(f'{i["type"]} "{i["number"]}" "{i["name"]}"')
    return


def add_new(n_doc, doc_type, name, n_shelf):
    res = False
    # if n_shelf not in directories.keys():
    #     directories[n_shelf] = [n_doc]
    if n_shelf in directories.keys():
        res = True
        for k, v in directories.items():
            if k == n_shelf:
                v.append(n_doc)
                documents.append({"type": doc_type, "number": n_doc, "name": name})
                break
    return res

def delete_user(n_doc):
    res = [False, False]
    for i in documents:
        if i["number"] == n_doc:
            documents.remove(i)
            res[0] = True
            break
    for k, v in directories.items():
        if n_doc in v:
            v.remove(n_doc)
            res[1] = True
            break
    return res

def move_to_new_shelf_by_n_doc(n_doc, n_shelf):
    res = [False, False, False]
    if (n_shelf in directories.keys()):
        res[0] = True
    if res[0]:
        for i in documents:
            if i["number"] == n_doc:
                res[1] = True
                break
    if res[1]:
        for k, v in directories.items():
            if n_doc in v:
                res[2] = True
                v.remove(n_doc)
                break
    if res[2]:
        for k, v in directories.items():
            if k == n_shelf:
                v.append(n_doc)
                break
    return res

def add_shelf_by_n(n_shelf):
    res = False
    if (n_shelf not in directories.keys()):
        directories[n_shelf] = []
        res = True
    return res

def get_comand():
    while True:
        comand = input()
        if comand == "p":
            n_doc = input("Введите номер документа! ")
            name = get_name_by_id(n_doc)
            if name != None:
                print(name)
            else:
                print("Нет такого документа!")
        elif comand == "s":
            n_doc = input("Введите номер документа! ")
            result = get_shelf_by_n_doc(n_doc)
            if result != None:
                print(result)
            else:
                print("Нет такого документа на полках!")
        elif comand == "l":
            print_doc()
        elif comand == "a":
            n_doc = input("Введите номер документа ")
            doc_type = input("Введите тип документа ")
            name = input("Введите имя ")
            n_shelf = input("Введите номер полки ")
            result = add_new(n_doc, doc_type, name, n_shelf)
            if result:
                print("Информация добавлена!")
            else:
                print("Полки не существует! Документ не добавлен!")
        elif comand == "d":
            n_doc = input("Введите номер документа! ")
            res_list = delete_user(n_doc)
            if (res_list[0] is False) and (res_list[1] is False):
                print("Нет такого номера в документах и на полках! ")
            elif (res_list[0] is True) and (res_list[1] is False):
                print("Удалено из документов, но на полке не было!")
            elif (res_list[0] is False) and (res_list[1] is True):
                print("Удалено с полки, но в документах не было!")
            else:
                print("Успешно удалено!")
        elif comand == "m":
            n_doc = input("Введите номер документа! ")
            n_shelf = input("Введите новую полку! ")
            result = move_to_new_shelf_by_n_doc(n_doc, n_shelf)
            if not result[0]:
                print("Нет такой полки!")
            elif not result[1]:
                print("Нет документа в базе!")
            elif not result[2]:
                print("Нет документа на полке!")
            else:
                print("Документ перенесён!")
        elif comand == "as":
            n_shelf = input("Введите номер новой полки! ")
            result = add_shelf_by_n(n_shelf)
            if result:
                print("Полка добавлена!")
            else:
                print("Полка уже существует!")
        elif comand == "q":
            break
        else:
            print("Введите правильную команду!")


if __name__ == '__main__':
    get_comand()
```
