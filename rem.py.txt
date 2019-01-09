import sqlite3
import subprocess as subpro   
import sys   
db=sqlite3.connect('newprjt.db')
cur=db.cursor()
def reminder():
	print("\n\nReminder Application!\nOptions:\n  1 : Create table 'reminder'\n  2 : Add reminders\n  3 : View reminders\n  4 : Update reminder\n 5 : Exit")
	option = input('Enter the option : ')
	if option == '1':

		
		
		try:        
		    cur =db.cursor()
		    cur.execute('''CREATE TABLE remin (
		    rID INTEGER PRIMARY KEY AUTOINCREMENT,
		    rTitle TEXT (20) NOT NULL,
		    rDateTime TEXT (20) NOT NULL);''')
		    print ('Reminder table created')
		except:
		    print ('Error')
		    db.rollback()
        reminder() 
	elif option == '2':
		
		rTitle = input('\nEnter Subject : ')
	    rDateTime = input('\nEnter reminder time in DD/MM/YYYY HH:MM:SS format : ')
		qry="insert into remin (rTitle, rDateTime) values('"+rTitle+"', '"+rDateTime+"');"
		try:
		    cur=db.cursor()
		    cur.execute(qry)
		    db.commit()
		    print ("\nReminder added ")
		except:
		    print ("\nOperation Failed!!!")
		    db.rollback()
		reminder() 
	
	elif option == '3':
		
		print("\n")
		sql="SELECT * from remin;"
		cur=db.cursor()
		cur.execute(sql)
		flag=False
	    data=cur.fetchall()
		for x in data:
			flag = True
			print(x)
		if flag == False:
			print("\nNo Data found")
		
		reminder() 
	elif option == '4':
		rID = input('\nEnter reminder Id : ')
		rTitle = input('\nEnter new reminder title : ')
		rDateTime = input('\nEnter new reminder time in DD/MM/YYYY HH:MM:SS format : ')
		qry="update remin set rTitle=?,rDateTime=? where rID=?;"
		try:
		    cur=db.cursor()
		    cur.execute(qry, (rTitle,rDateTime,rID))
		    db.commit()

		    print("\nReminder updated ")
		except:
		    print("\nUpdation Error")
		    db.rollback()
	    reminder()
	elif option == '5':
		db.close()
		print("Thank you for using our application")
		sys.exit()
	else:
		print("Failed")

reminder() 







 
