# Superset: Task 5

## Files:

* `./superset/utils/core.py` line: 875-988
* `./superset/reports/notifications/email.py` for email template and format then sending it uses utility function
* `./superset/reports/notifications/__init__.py` @create_notification
* `./superset/reports/commands/execute.py` BaseReportState._send
* `./superset/tasks/scheduler.py` line: 80

## Execution flow

1. Scheduler [`./superset/tasks/scheduler.py`]
    In this file there is two celery tasks are defined

    | task | name |
    | --- | --- |
    | scheduler | reports.scheduler |
    | execute | reports.execute |

    * **scheduler**: checks for active report schedules and triggers the `execute` task
    * **execute**: generate reports and then sends emails. The execute task runs the report schedule. This code is then initiates the next flow

    ```python
    AsyncExecuteReportScheduleCommand(
        task_id,
        report_schedule_id,
        scheduled_dttm,
    ).run()
    ```

2. Handling various states of the reporting like Working, not triggered, success
    * The `AsyncExecuteReportScheduleCommand.run()` method triggered `ReportScheduleStateMachine.run()` method which actually handles all the lifecycle states `[ReportWorkingState, ReportNotTriggeredErrorState, ReportSuccessState]`
    * `ReportSuccessState.next()` method then triggered the `_send()` method which is responsible for collecting data, preparing mail then send

3. `BaseReportState` is a plarent class which is parent class for all different states, responsible for managing the reports lifecycle. This have all methods which is required in the reports lifecycle.

    This class have 3 child classes which are responsible for managing the various states.
    * ReportWorkingState
    * ReportNotTriggeredErrorState
    * ReportSuccessState

    Methods:
    * `_get_screenshots`
    * `_get_csv_data`
    * `_get_notification_content`
    * `update_report_schedule_and_log`: updates the report schedule and logs the report schedule state change.
    * `is_in_grace_period, is_in_error_grace_period, is_on_working_timeout`. This methods is for checking for which states

4. `BaseReportState.send()` method Creates the notification content and sends them to all recipients
5. `_get_notification_content`: It returns the instance of **NotificationContent**, based on the type of required data formats image, csv, or text
6. `_get_csv_data`: It fetches the data using its url then return it as bytes
7. `BaseNotification`: This is a parent class for all notification classes.
8. `EmailNotification`: This is the implementation of `BaseNotification` class for handling email notification.
9. `EmailNotification` has various methods
    * `send`: This method is responsible for sending the email
    * `get_content`: This method is responsible for getting the content of the email
    * `get_subject`: This method is responsible for getting the subject of the email
    * `_get_to`: This method is responsible for getting the recipients of the email
    * `_get_smtp_domain`: This method is responsible for getting the smtp server of the from_email

10. `send_smtp_email`: This is utility method, responsible for sending the email using smtplib library. defined in the file `./superset/utils/core.py` line: 875-988

## Code snippet to send email in python

```py
def send(sub, body, recipant):
    msg = MIMEMultipart()
    msg['From'] = "purushottam.khedre@hotwaxsystems.com"
    msg['To'] = recipant
    msg['Subject'] = sub
    msg.attach(MIMEText(body, 'plain'))
    
    server = smtplib.SMTP("smtp.gmail.com", 587)
    server.starttls()
    server.login("purushottam.khedre@hotwaxsystems.com", "phggciqiwlfkgseu")
    text = msg.as_string()
    server.sendmail("purushottam.khedre@hotwaxsystems.com", recipant, text)
    server.quit()

send("Testing", "This is a test email body.", "purushottamkhedre123@gmail.com")
```
