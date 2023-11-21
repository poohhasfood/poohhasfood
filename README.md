
import tkinter as tk
from tkinter import ttk
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

class EmailAutomationApp:
    def __init__(self,master):
        self.master = master
        self.master.title("Email Automation App")

        self.setup_ui()

 #create and place widgets
    def setup_ui(self):
        self.label_name = tk.Label(self.master, text="Enter your Name:")
        self.label_name.grid(row=0, column=0, sticky="E", padx=5, pady=5)

        self.entry_name = tk.Entry(self.master, width=50)
        self.entry_name.grid(row=1, column=0, columnspan=2, padx=5, pady=5)

        self.label_enrollmentnumber = tk.Label(self.master, text="Enter your enrollment number:")
        self.label_enrollmentnumber.grid(row=0, column=1, sticky="E", padx=5, pady=5)

        self.entry_enrollmentnumber = tk.Entry(self.master, width=50)
        self.entry_enrollmentnumber.grid(row=1, column=2, columnspan=2, padx=5, pady=5)

        self.label_blockno = tk.Label(self.master, text="Enter your block number:")
        self.label_blockno.grid(row=0, column=3, sticky="E", padx=5, pady=5)

        self.entry_blockno = tk.Entry(self.master, width=50)
        self.entry_blockno.grid(row=1, column=3, columnspan=2, padx=5, pady=5)

        self.label_roomno = tk.Label(self.master, text="Enter your room number:")
        self.label_roomno.grid(row=0, column=4, sticky="E", padx=5, pady=5)
       
        self.entry_roomno = tk.Entry(self.master, width=50)
        self.entry_roomno.grid(row=1, column=4, columnspan=2, padx=5, pady=5)

        self.label_password = tk.Label(self.master, text="Enter your password:")
        self.label_password.grid(row=0, column=5, sticky="E", padx=5, pady=5)

        self.entry_password = tk.Entry(self.master, width=50)
        self.entry_password.grid(row=1, column=5, columnspan=2, padx=5, pady=5)

        self.label_issue = tk.Label(self.master, text="choose your issue from below list:")
        self.label_issue.grid(row=0, column=6, sticky="E")

        self.entry_issue = tk.Entry(self.master, width=50)
        self.entry_issue.grid(row=1, column=6, columnspan=2, padx=5, pady=5)
        
        self.button_send = tk.Button(self.master, text="Send Email", command=self.send_email)
        self.button_send.grid(row=0, column=8, sticky="E")

        
        #get values from the UI components 
    def send_email(self):
        to_address = self.entry_to.get()
        subject = self.entry_subject.get()
        body = self.text_body.get("1.0", tk.end)
    
         #create MIME message 
        msg = MIMEMultipart('alternative')
        msg['From'] = sender_email
        msg['To'] = recipient_email
        msg['CC'] = ",".join(cc)
        msg['Subject'] = subject 
        message.attach(MIMEText(body,"plain"))

         #connect to the SMTP server
        smtp_server = 'smtp-mail.outlook.com'
        smtp_port = 587
        
        try:
            recipient_emails = [recipient_email] + cc
           # Create a secure SSL/TLS connection to the SMTP server
            server = smtplib.SMTP(smtp_server, smtp_port)
            server.starttls()

            # Login to your Outlook email account
            server.login(sender_email, sender_password)

            # Send the email
            server.sendmail(sender_email, recipient_emails, msg.as_string())

            print("Email sent successfully!")

        except smtplib.SMTPException as e:
        print("Error sending email:", str(e))
            
        finally:
             # Close the connection to the SMTP server
                server.quit()
           
            #create the mainapplication window
        root = tk.Tk()
        app = EmailAutomationApp(root)
        root.mainloop()
