# Railway-Ticket-Management-System

#PROJECT MEMBERS - R.Y. SRIKAANTH (RA2311003011211) & Navam Endlay (RA2311003011207)
<br>
import smtplib
<br>
from email.mime.multipart import MIMEMultipart
<br>
from email.mime.text import MIMEText
<br>
from email.mime.base import MIMEBase
<br>
from email import encoders
<br>


def sendmail(name,phno,age,gender,trainno,fr,to,date,email):
<br>
    msg = MIMEMultipart()
<br>
    msg['From'] = "srikaanth2005@gmail.com"
<br>
    msg['To'] = email
<br>
    msg['Subject'] = "Railway booking confirmation."
<br>

    # string to store the body of the mail
    body = f"Name : {name}\nPhone number : {phno}\nAge: {age}\nGender: {gender}\nTrain No.: {trainno}\nDeparture: {fr}\nDestination: {to}\nDate: {date}"
    msg.attach(MIMEText(body, 'plain'))
    s = smtplib.SMTP('smtp.gmail.com', 587)
    s.starttls()

    # Authentication
    s.login("srikaanth2005@gmail.com", "mmnhbidwjvoyqpeb")

    # Converts the Multipart msg into a string
    text = msg.as_string()

    # sending the mail
    s.sendmail(msg['From'], msg['To'], text)

    # terminating the session
    s.quit()
#sendmail("AAA",12345,23,"M",23456,"MAS","CBE","12-03-2023","srikaanth2005@gmail.com")
########################################################################## RAILWAY TICKET RESERVATION PROJECT (CLASS-XII) #################################################################################
```from pywhatkit import sendwhatmsg_instantly
from random import randint
from Mail1 import sendmail
def menu():
    print('1.YES')
    print('2.NO')
    ch=int(input('DO YOU WANT TO CONTINUE OR NOT:'))
    while ch==1:
        print('WELECOME TO ONLINE RAILWAY RESERVATION SYSTEM') 
        print('1.SIGN IN')
        print('2.SIGN UP')
        print('3.EXIT')
        ch1=int(input('ENTER YOUR CHOICE:'))
        if ch1==1:
            a=checking_2()
            if a==True:
                print('WELCOME')
                main()
            else:
                
                continue
        elif ch1==2:
            a=checking_1()
            if a==True:
                main()
            else:
                print('USERNAME ALREADY EXISTS')
                continue
        elif ch1==3:
            print('THANK YOU')
            break
        else:
            print('ERROR 404:PAGE NOT FOUND')
            break
```
```def main():        
    print('1.yes')
    print('2.no')
    c=int(input("do you want to continue or not:"))
    while (c==1):
        print(' 1.TICKET BOOKING',"\n", '2.TICKET CHECKING',"\n",'3.TICKET CANCELLING',"\n",'4.ACCOUNT DETAILS',"\n",'5.LOG OUT')
        ch=int(input('enter ur choice:'))
        if ch==1:
            ticket_booking()
        elif ch==2:
            ticket_checking()
        elif ch==3:
            ticket_cancelling()
        elif ch==4:
            checking_3()
            
                
        elif ch==5:
            print('THANK YOU')
            break
        else:
            print('WRONG INPUT')
    else:
        print('ERROR 404: ERROR PAGE NOT FOUND')
```
```def ticket_booking():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    fr=input('enter your starting point:')
    to=input('enter your destination:')
    date=input('enter date(DD-MM-YYYY):')
    cursor.execute("select * from trains where source='{}' and destination='{}'".format(fr,to))
    result=cursor.fetchall()
    for i in result:
        print(i)
    choice1=input("DO YOU WANT TO BOOK TICKETS?:YES/NO")
    if choice1=="YES":
        seats = int(input("Enter the number of seats:"))
        trainno = int(input("Enter the train numner:"))
        cursor.execute("select seats from trains where trainno = {}".format(trainno))
        result=cursor.fetchone()
        if result[0]>=seats:
            print("Tickets available. Enter your details")    
            name=input('enter your name:')
            phno=input('enter your phone number:')
            age=int(input('enter your age:'))
            print(' M=MALE','\n','F=FEMALE','\n','N=NOT TO MENTION')
            gender=input('enter your gender:')
            Gender=gender.upper()
            a={'M':'MALE','F':'FEMALE','N':'NOT TO MENTION'}
            v=a[Gender]
            s1="insert into railway values('{}',{},{},'{}','{}','{}','{}')".format(name,phno,age,v,fr,to,date)
            cursor.execute(s1)
            print("")            
            print('BOOKED SUCCESSFULLY')
            email=input("Enter your emailID:")
            sendmail(name,phno,age,gender,trainno,fr,to,date,email)
            cursor.execute("update trains set seats=seats-{} where trainno={}".format(seats,trainno))
        else:
            print("Tickets not available")
```
        
```def ticket_checking():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    print('1.yes')
    print('2.no')
    ch=int(input("Do you want to continue or not:"))

    if ch==1:
        phno=int(input('Enter your phone number:'))
        try:
            s1="select * from railway where phno={}".format(phno)
            cursor.execute(s1)
            data=cursor.fetchall()[0]
            Data=list(data)
            a=['NAME','PHONE NUMBER','AGE','GENDER','STARTING POINT','DESTINATION','DATE',]
            print(a[0],'::::',Data[0].upper())
            print(a[1],'::::',Data[1])
            print(a[2],'::::',Data[2])
            print(a[3],'::::',Data[3].upper())
            print(a[4],'::::',Data[4].upper())
            print(a[5],'::::',Data[5].upper())
            print(a[6],'::::',Data[6])
        except:
            print('TICKET DOES NOT EXISTS')
    elif ch==2:
        print('THANK YOU')
    else:
        print('ERROR 404:PAGE NOT FOUND')
```    
       

```def ticket_cancelling():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    phno=input('Enter your phone number:')
    s1="delete from railway where phno={}".format(phno)
    cursor.execute(s1)
    print('TICKET CANCELLED')
```
        
```def checking_2():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    a=input('USER NAME:')
    choice=int(input("1.Login using OTP \n2.Login using password \nEnter your choice:"))
    if choice==1:
        phnum=input("Enter your Phone no along with country code:")
        try:
            key=str(randint(1000,9999))
            sendwhatmsg_instantly(phnum,"Login using "+key,tab_close=True)
            otp=input("Enter the OTP sent to {0}:".format(phnum))
            if key==otp:
                return True
            else:
                print("Invalid OTP")
        except:
            print("Error in sending the OTP.Please check whether the given Phone no exists in Whatsapp")
    elif choice==2:
        b=input('PASS WORD:')
        #try:
        s1 = "select password from user_accounts where user_name='{}'".format(a)
        cursor.execute(s1)
        data = cursor.fetchall()[0][0]
        print(data)
        if data == b:
            return True
        else:
            print('ERROR 404:PAGE NOT FOUND')
    
    return False
 ```       

def checking_1():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    f=input("FIRST NAME:")
    l=input("LAST NAME:")
    n=f+" "+l
    a=input('USER NAME:')
    b=input('PASS WORD:')
    c=input('RE-ENTER YOUR PASS WORD:')
    ph=input("PHONE NUMBER:")
    print(' M=MALE','\n','F=FEMALE','\n','N=NOT TO MENTION')
    gen=input('ENTER YOUR GENDER:')
    print("ENTER YOUR DATE OF BIRTH")
    d=input("DD:")
    o=input("MM:")
    p=input("YYYY:")
    dob=d+'/'+o+'/'+p
    age=input('YOUR AGE:')
    v={'M':'MALE','F':'FEMALE','N':'NOT TO MENTION'}
    if b==c:
        
        c1="insert into user_accounts values('{}','{}','{}','{}',{},'{}','{}',{})".format(f,l,a,b,ph,v[gen],dob,age)
        cursor.execute(c1)
        print('WELCOME',f,' ',l)
        return True
        #except:
            #print('PASSWORD ALREADY EXISTS')
            #return False
    else:
        print('BOTH PASSWORDS ARE NOT MATCHING')
        


def checking():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    a=input('USER NAME:')
    b=input('PASS WORD:')
    try:
        s1="select user_name from user_accounts where password='{}'".format(b)
        c1="select fname,lname from user_accounts where password='{}'".format(b)
        cursor.execute(c1)
        data1=cursor.fetchall()[0]
        
        data1=list(data1)
        data1=data1[0]+' '+data1[1]
        cursor.execute(s1)
        data=cursor.fetchall()[0]
        data=list(data)[0]
        if data==a:
            print(' HII ',data1)
            return True
        else:
            return False
    except:
        print('ACCOUNT DOES NOT EXIST')

def checking_3():
    import mysql.connector
    mycon=mysql.connector.connect(host='localhost',user='root',passwd='browse@123',database='railway')
    cursor=mycon.cursor()
    mycon.autocommit=True
    a=input('USER NAME:')
    b=input('PASS WORD:')
    try:
        s1="select user_name from user_accounts where password='{}'".format(b)
        c1="select fname,lname from user_accounts where password='{}'".format(b)
        cursor.execute(c1)
        data1=cursor.fetchall()[0]
        data1=list(data1)
        data1=data1[0]+' '+data1[1]
        cursor.execute(s1)
        data=cursor.fetchall()[0]
        data=list(data)
        if data[0]==a:
            
            x=['FIRST NAME','LAST NAME','PHONE NUMBER','GENDER','DATE OF BIRTH','AGE']
            s1="select fname,lname,phno,gender,dob,age from user_accounts where password='{}'".format(b)
            cursor.execute(s1)
            data=cursor.fetchall()[0]
            data=list(data)
            print(x[0],':::',data[0])
            print(x[1],':::',data[1])
            print(x[2],':::',data[2])
            print(x[3],':::',data[3])
            print(x[4],':::',data[4])
            print(x[5],':::',data[5])
            
            
        else:
            return False
    except:
        print('ACCOUNT DOES NOT EXIST')

menu()
#ticket_booking()
