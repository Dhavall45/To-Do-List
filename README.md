# To-Do-List
from tkinter import *
import tkinter.messagebox
def add_task():
    global entry_task  
    input_text = entry_task.get(1.0, "end-1c")
    if input_text == "":
        tkinter.messagebox.showwarning(title="Warning!", message="Please Enter some Text")
    else:
        listbox_task.insert(END, input_text)
        root_add_task.destroy()
        
        
def enter_task():
    global entry_task, root_add_task
    root_add_task = Tk()
    root_add_task.title("Add your task here")
    
    entry_task = Text(root_add_task, width=60, height=8)
    entry_task.pack()
    
    button_add_task = Button(root_add_task, text="Add your task", command=add_task)
    button_add_task.pack()
    
    root_add_task.mainloop()

    
def delete_task():
    selected = listbox_task.curselection()
    if selected:
        listbox_task.delete(selected[0])
        
        
def mark_completed():
    selected = listbox_task.curselection()
    if selected:
        temp_index = selected[0]
        temp_text = listbox_task.get(temp_index)
        updated_text = temp_text + "✅ Task complated"
        listbox_task.delete(temp_index)
        listbox_task.insert(temp_index, updated_text)
        
        
window = Tk()
window.title("To-Do List Application")
frame_task = Frame(window)
frame_task.pack()

listbox_task = Listbox(frame_task, bg="black", fg="white", height=20, width=50,font="Font")
listbox_task.pack(side=RIGHT)
scrollbar_task = Scrollbar(frame_task)
scrollbar_task.pack(side=RIGHT, fill=Y)
listbox_task.config(yscrollcommand=scrollbar_task.set)
scrollbar_task.config(command=listbox_task.yview)



add_button = Button(window, text="Add Task", width=40, command=enter_task)
add_button.pack(pady=3)

delete_button = Button(window, text="Delete Task", width=40, command=delete_task)
delete_button.pack(pady=3)

mark_button = Button(window, text="Completed Task", width=40, command=mark_completed)
mark_button.pack(pady=3)
window.mainloop()
