# concatenator
file concatenator with timestamp
import os
from Tkinter import *
import Tkinter, tkFileDialog
import datetime

def timeStamped(fname, fmt='%Y-%m-%d-%H-%M-%S_{fname}'):
    return datetime.datetime.now().strftime(fmt).format(fname=fname)


root = Tk()
root.withdraw()
current_directory = tkFileDialog.askdirectory()
##root.filename = tkFileDialog.askopenfilename(initialdir = "/",title = "Select file",filetypes = (("text files","*.txt"),("all files","*.*")))


## Maybe add a TK file selection box here. 
os.chdir(current_directory)
print(os.getcwd())
outputFile = open(timeStamped("output"), "a+")


#print(os.listdir("."))
filelist = (os.listdir(current_directory))
for file in filelist:
    print(file)
    if file.startswith("RSD"):
        f = open(file, "r")
        outputFile.write(f.read())
        f.close()
        os.unlink(os.path.join(current_directory,file))
                  
outputFile.close()
