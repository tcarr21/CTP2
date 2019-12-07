#The Optimistic 5??? (For a Group Name)
#program that sends reminders of when a task needs to be completed and has motivational messages sent twice a day. 
#no I think the effort put into the name Good 'ol Group 4 is too great - Garrett 

#start of program...code

"""
Good 'ol Group Four
Taviana Carr, Garrett Naylon, Hannah Connolly, Trenton Davis, and Griffin Ewers
CRN:15310
Section 003
Due: December 7th, 2019
"""
#doc string, just states project and my name
print(__doc__)
#imports datetime, so it can be used
import datetime

#welcomes user to application
print("Welcome to M & R = Motivation & Reminders! Here you will be able to get friendly reminders to stay on track and some daily motivation to stay positive!\n")
#lines 16-17 allows for user to input their name
h=input("What is your name? ")
print("Nice to see you today",h)

#getting the exact day from the datetime module
tday=datetime.date.today()

print(tday,"\n")

#list of daily quotes 
quotes=[
       "Have a great day! There may be many challenges facing you, but do not give up and remember to smile!",
       "You are strong, cappable, and intellignet, today will be great and do not let anything deter you!",
       "Today is a new day, forget yesterday, it is over. Focus on ways to better yourself and those around you.",
       "Remember it is okay to have time to yourself and to make time for for your mental and physical health, that is all you have, the longevity of your health starts with you.",
       "Greetings, today take a moment and write down how you are feeling so far and write down 5 things that you are grateful for.",
       "Hi, it's your off day, go to sleep,exercise, spend time with family or your significant other! Enjoy your day off and do something for yourself.",
       "Smile and be joyful, there is so much to live for, anything that is currently bothering you will pass. Destress and spend some time today meditating!"]
#lines 37-65 are identifiying weekdays and printing out messages depending on the day.
#weekday=day of week and tday=current day of the week the program is ran on
# "==" means if something is equal to another variable 
def reminder():
    """This is making it possible to use the weekdays and say a certain message on a given day"""
    if tday.weekday()==0:
        return_value=quotes.pop(0)
        #pop feature is used so that messages are not repeated
        print('',return_value)
    elif tday.weekday()==1:
        return_value=quotes.pop(2)
        print('', return_value)
    elif tday.weekday()==2:
        return_value=quotes.pop(1)
        print('', return_value)
    elif tday.weekday()==3:
        return_value=quotes.pop(3)
        print('',return_value)
    elif tday.weekday()==4: 
        return_value=quotes.pop(4)
        print('',return_value)
    elif tday.weekday()==5:
        return_value=quotes.pop(5)
        print('',return_value)
    elif tday.weekday()==6:
        return_value=quotes.pop(6)
        print('',return_value)
    else:
        print()  

print(reminder.__doc__)
#prints docstring
print("\n")
#prints a space for aesthetic purposes
        
reminder()
#prints the reminder for the day (motivational message)
print("\n")

print("Today you need to...")

data=pd.read_csv('C:/Users/tavia/Downloads/task216.csv')
type(data)
mylist=data['tas'].tolist()
type(mylist)

def task1():
    """ Says what task need to be done for a given day of the week"""
    if tday.weekday()==0:
        print(mylist[0:2])
    elif tday.weekday()==1:
        print(mylist[3:5])
    elif tday.weekday()==2:
        print(mylist[6:8])
    elif tday.weekday()==3:
        print(mylist[9:11])
    elif tday.weekday()==4:
        print(mylist[12:14])
    elif tday.weekday()==5:
        print(mylist[15:17]) 
    elif tday.weekday()==6:
        print(mylist[18:20])
    else:
        print()
#prints the task assigned for the day        
task1()

import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

email= 'notifacationprojectCTP@gmail.com'
#who you should be getting the eamil from
password= 'CTP42project$'
send_to_email= 'gewers@kent.edu'
#sends email to this adress- can change it.
subject= 'notifacation application'
message= 'test' 

msg=MIMEMultipart()
msg ['from']=email 
msg ['To']=send_to_email
msg['subject']= subject

def attach(): 
    msg.attach(MIMEText(reminder,task1,'plain'))

server= smtplib.SMTP('smtp.gmail.com',587)
server.starttls()
server.login(email,password)
text=msg.as_string()

def send():
    server.sendmail(email,send_to_email,text)

server.quit()

import schedule
import time
"""NOTE: schedule and schedule.py are different. schedule.py will override the scheudle module and cuse an error that says "module 'schedule' has no attribute 'every'" even though it does. make sure schedule.py isn't overriding. Thats how I got it to work.It was a big headache."""
#imports the scheduling module 

schedule.every().day.at("08:00").do(attach)
schedule.every().day.at("08:00").do(send)
#every day at 8am it will attach the days tasks and reminders to the email and then send them

while True:
   S = schedule.run_pending()
   time.sleep(1)
   if S==ord("*"):
        break
#by entering the * key it cancels the program. also i put in a time for it to rest. although this can be taken out :)
