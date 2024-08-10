Code Breakdown
Imports

python
Copy code
import time
import webbrowser
from plyer import notification
time: Used for getting the current time.
webbrowser: Opens a web browser to visit a URL.
plyer.notification: Provides a cross-platform way to show desktop notifications.
watch_browser Function


def watch_browser():
    times = time.strftime("%H:%M:%S")
    print("Time Is Recorded :", times)
Purpose: Prints the current time when a suspicious activity is detected.
Details: Uses time.strftime to get the current time in HH:MM:SS format and prints it.
notify_suspicious Function

def notify_suspicious():
    notification.notify(
        title="Warning",
        message="You can't search suspicious websites!",
    )
    watch_browser()
    quit()
Purpose: Shows a notification and logs the time when a suspicious website is detected.
Details: Displays a notification with a warning message and then calls watch_browser to log the time. The quit() function terminates the program.
suspicious_website Function


def suspicious_website(user):
    # List of suspicious keywords
    suspicious_keywords = [
        "free", "offer", "credit", "winner", "urgent", ...
    ]

    # List of suspicious file extensions
    suspicious_extensions = [
        ".exe", ".bat", ".cmd", ".scr", ".pif", ...
    ]

    for keyword in suspicious_keywords:
        if keyword in user.lower():
            return True
    
    for extension in suspicious_extensions:
        if user.lower().endswith(extension):
            return True
    return False
Purpose: Checks if the provided URL or file name contains suspicious keywords or extensions.
Details:
Keywords: Contains a list of suspicious terms often associated with scams or phishing sites.
Extensions: Contains a list of file extensions commonly associated with malware.
Logic: Converts the user input to lowercase and checks if it contains any suspicious keywords or ends with any suspicious file extensions. If a match is found, it returns True; otherwise, False.
user_input Function


def user_input():
    while True:
        print("\n__________Press 'q' for Quit__________\n")
        user = input("Paste or Enter the Website Name : ")

        if suspicious_website(user):
            notify_suspicious()

        elif user.lower() == "q":
            print("Quitting the Website. . . ")
            exit()

        else:
            web = webbrowser.open(f"https://{user}")
            print("This is a safe website.")
Purpose: Continuously prompts the user to enter a website URL and checks if it is suspicious.
Details:
Input: Takes user input for a website URL or file name.
Suspicious Check: Calls suspicious_website() to determine if the input is suspicious. If it is, triggers notify_suspicious().
Exit: If the user types "q", the program prints a quitting message and exits.
Safe Websites: Opens the URL in a web browser if it is deemed safe.
Summary
🔍 The code monitors user input for suspicious website names or file extensions, using predefined lists of keywords and extensions.
🔔 It issues a warning notification and logs the time if suspicious activity is detected.
🌐 If the input is not suspicious, it opens the provided URL in a web browser.
🚪 Users can exit the program by entering 'q'.
This code is a simple yet effective tool for alerting users about potentially harmful websites or files based on common characteristics of such threats.
