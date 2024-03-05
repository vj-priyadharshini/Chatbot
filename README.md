from tkinter import *
from chatterbot import ChatBot
from chatterbot.trainers import ListTrainer


bot=ChatBot('Bot')
trainer=ListTrainer(bot)

data=open('test.yaml','r',encoding='utf-8').readlines()

trainer.train(data)

def botReply():
    question=questionField.get()
    answer=bot.get_response(question)
    textarea.insert(END,'You: '+question)
    textarea.insert(END,'Bot: '+answer)
    questionField.delete(0,END)



root=Tk()

root.geometry('500x570+100+30')
root.title('Talking ChatBot')
root.config(bg='violet')

logoPic=PhotoImage(file='pic.png')

logoPicLabel=Label(root,image=logoPic,bg='violet')
logoPicLabel.pack(pady=5)

centerFrame=Frame(root)
centerFrame.pack()

scrollbar=Scrollbar(centerFrame)
scrollbar.pack(side=RIGHT)

textarea=Text(centerFrame,font=('times new roman',20,'bold'),height=10,yscrollcommand=scrollbar.set
              ,wrap='word')
textarea.pack(side=LEFT)
scrollbar.config(command=textarea.yview)

questionField=Entry(root,font=('verdana',20,'bold'))
questionField.pack(pady=15,fill=X)

askPic=PhotoImage(file='ask.png')


askButton=Button(root,image=askPic,command=botReply)
askButton.pack()

root.mainloop()
