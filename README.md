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

#getting the exact day from the datetime module
tday=datetime.date.today()

print(tday,"\n")

#lines 20-35 are identifiying weekdays and printing out messages depending on the day.
#weekday=day of week and tday=current day of the week the program is ran on
# "==" means if something is equal to another variable 
def reminder():
    """This is making it possible to use the weekdays and say a certain message on a given day"""
    if tday.weekday()==0:
        print("Don't give up! Everything will be okay. This can be a long drawn out day for some, but for you, it will be so rewardsing! Change your mindset on how this day is viewed! \n") 
    elif tday.weekday()==1:
        print("You are beautiful! Do not let others get the best of you! Take a few minutes to breathe and admire the scenary or just the beauty in life.\n")
    elif tday.weekday()==2:
        print("Smile through the pain, it never rains forever! What are some areas of imporovemet for you?\n")
    elif tday.weekday()==3:
        print("It's almost Friday! Write down how you are feeling so far and take a moment to write down 5 things that made you smile!\n")
    elif tday.weekday()==4: 
        print("You should be so proud of yourself, look how far you have come! Yes there may have been sometimes where you felt down, but go celebrate yourself, you deserve it!\n")
    elif tday.weekday()==5:
        print("Take the time to relax and unwind. What are you greatful for? Sit down and write down your thoughts and feelings on this.\n")
    else:
        print("Go to sleep! Enjoy your day off and do something for yourself. \n")  
#print(reminder.__doc__)
        
#prints the reminder for the day (motivational message)
reminder()

#lines 45-68 are giving task reminders to the user on the given day the program is ran, so that they stay productive
# "==" means if something is equal to another variable 
def task1():
    """ Says what task need to be done for a given day of the week"""
    if tday.weekday()==0:
       print("Clean room at 4:00 p.m.")
       print("Cook dinner at 4:45 p.m.")
       print("Do homework at 7:30 p.m.\n")
    elif tday.weekday()==1:
        print("Exercise this morning at 6:00 a.m.")
        print("Go to tutoring at 12:05 p.m.")
        print("Make time for yourself and plan out 30 minutes of quiet time. \n")
    elif tday.weekday()==2:
        print("Go to grocery store today, budget $100")
        print("Study for classes between, 6:30 p.m.-10:00 p.m.")
    elif tday.weekday()==3:
        print("Pick up daughter from soccer practice at 5:30 p.m.")
        print("Go to gym at 8:00 p.m.\n")
    elif tday.weekday()==4:
        print("Go to bank to get your bouns and plan family vaction! Save $250 a week!")
        print("Put your phone on Do Not Disturb at 6:00 p.m. and relax.\n")
    elif tday.weekday()==5:
        print("Go shopping, budget is $300")
        print("Go on date\n")
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
