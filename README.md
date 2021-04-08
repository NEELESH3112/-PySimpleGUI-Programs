# -PySimpleGUI-Programs
import PySimpleGUI as sg
from file_ops import file_write, file_read

tasks = file_read('todolist.txt')

layout = [
    [sg.InputText("", size=(40,1), font=('Arial', 18), key='add_item'),
      sg.Button("Add", font=('Arial', 18), key='add_save')],
    [sg.Listbox(values=tasks, size=(40,10), font=('Arial', 18), key='items'),
      sg.Button("Edit", font=('Arial', 18), key='edit'),
      sg.Button("Delete", font=('Arial', 18), key='delete')]

]

def add_item():
    item = values['add_item']
    tasks.append(item)
    window.FindElement('items').Update(values=tasks)
    window.FindElement('add_item').Update("")
    window.FindElement('add_save').Update("Add")


def delete_item():
    delete_val = values['items'][0]
    tasks.remove(delete_val)
    window.FindElement('items').Update(values=tasks)


def edit_item():
    edit_val = values['items'][0]
    tasks.remove(edit_val)
    window.FindElement('items').Update(values=tasks)
    window.FindElement('add_item').Update(value=edit_val)
    window.FindElement('add_save').Update("Save")


window = sg.Window("Todolist", layout)
while True:
    event, values = window.Read()
    if event == sg.WINDOW_CLOSED:
        break
    elif event == 'add_save':
        add_item()
    elif event == 'delete':
        delete_item()
    elif event == 'edit':
        edit_item()

file_write('todolist.txt', tasks)
