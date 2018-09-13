# GUI-Interface-for-python
import tkinter.filedialog as filedialog
import tkinter as tk
from configparser import ConfigParser
from tkinter import ttk

from tools import Tools

# XMLData.Get_Analysis_Link(b)
# XMLData.Running()

class Interface_XML2Excel():
    def __init__(self):
        self.XML_file = None
        self.Excel_file = None

        self.root = tk.Tk()
        self.root.title('ReportAnalysis')
        self.root.geometry('600x200+450+200')
        # Init Frame for all sub-windows
        container = tk.Frame(self.root)
        container.pack(side="top", fill="both", expand=True)
        container.grid_rowconfigure(0, weight=1)
        container.grid_columnconfigure(0, weight=1)

        # set up all sub-windows use the main frame and arrange them on the main object
        self.sub_windows = {}
        for sub_window in (Choose_Funcktion_Window, Choose_File_Window, Converting_Excel, Show_Progress_Window,
                           Choose_Measurement_Window):
            window_name = sub_window.__name__
            window = sub_window(parent=container, controller=self)
            self.sub_windows[window_name] = window
            window.grid(row=0, column=0, sticky="nsew")
        self.show_window("Choose_Funcktion_Window")

    def show_window(self, page_name):
        '''Show a frame for the given page name'''
        sub_window = self.sub_windows[page_name]
        sub_window.tkraise()

class Choose_Funcktion_Window(tk.Frame):
    def __init__(self, parent, controller):
        tk.Frame.__init__(self, parent)
        self.controller = controller
        FrameTable = tk.Frame(self)
        frm_Top = tk.Frame(FrameTable)
        tk.Label(frm_Top, text='Porsche', font=('Porsche Design Font', 14)).pack(pady=15)
        frm_Top.pack(side=tk.TOP)
        frm_Bottom = tk.Frame(FrameTable)
        tk.Button(frm_Bottom, text='Report Generator', command=self.Report_Generator).pack(side=tk.LEFT, padx=10, pady=50)
        # tk.Button(frm_Bottom, text='Merge FSM and FEM', command=self.Merge_FSM_and_FEM).pack(side=tk.LEFT, padx=10, pady=50)
        frm_Bottom.pack(side=tk.BOTTOM)
        FrameTable.pack()

    def Report_Generator(self):
        self.controller.show_window('Choose_File_Window')
