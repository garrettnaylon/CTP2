"""
Garrett Naylon
DSCI 15310
Section 003
@author: Garrett
"""
print (__doc__)

import datetime
#imports datetime module so that the computer knows the when/if the date changes
tday = datetime.date.today()
#this is for myself so I know if It is running 
print (tday, /n)

import schedule
#imports the scheduling module 
def email():
    """ this will be the thing that sends out the email with the quote"""
    print ("add the email portion here")
    
schedule.every().day.at("08:00").do(email)
#every day at 8am it will send this to def email.
#more can be added to do the task at other times

while True:
   S = schedule.run_pending()
   if S==ord("*"):
        break
#while loop keeps schedule running unless the key "*" is entered then the program will shut off.



