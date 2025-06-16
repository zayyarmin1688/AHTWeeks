Purpose

To streamline event management by:

Pulling form data stored in Google Sheets
Validating entries marked as “Valid Event?”
Creating new events in Google Calendar with rich metadata (title, description, location, etc.)
Updating calendar visibility and color based on confirmation status
Removing outdated events that are no longer valid

How It Works

Form Submissions → Sheet

Google Form responses populate a Google Sheet. Events marked as “Valid Event?” (column index 23) are considered for calendar upload.

Script Execution (main)

Reads all valid rows from the sheet
Checks if the event already exists in the calendar
Creates new calendar events if missing
Removes calendar events that no longer appear in the sheet

Time Handling (mergeDateAndTime)

Combines a date and a time string (e.g., "12:00 PM") into a Date object, handling edge cases like "12:00 AM" correctly.
Event Customization (updateCalendar)
Sets event title, location, description (with audience and notes), color, and visibility
Green/Public for confirmed events; Red/Private otherwise
Validation Cleanup (validationCheck)
Ensures the calendar contains only events present in the current spreadsheet by title comparison.
Sheet Structure Expectations



The script assumes:

Row 0 contains headers
Column 4 = Title
Column 5 = Description
Column 6 = Confirmed Date
Column 7 = Start Time (e.g., "11:00 AM")
Column 8 = End Time
Column 9 = Location
Column 14 = Target Audience
Column 16 = Extra Notes
Column 22 = Confirmation (truthy/falsy)
Column 23 = Valid Event? (must be true or truthy to include the row)

Setup Instructions

Link your Google Form to a Google Sheet.
Open the Google Sheet → Extensions → Apps Script.
Paste this script and replace nuciCalendarID with your own Google Calendar ID.
Save and run main() manually or via time-based trigger (e.g., every hour).
Ensure the script has the necessary permissions to read Sheets and modify Calendar.

Permissions Required

SpreadsheetApp: To read data from the Google Sheet
CalendarApp: To create, update, and delete calendar events
You will be prompted to authorize these scopes the first time the script runs.

Notes

Events are matched by title to avoid duplicates.
Time strings must be well-formatted (e.g., "9:00 AM", "12:15 PM") for accurate parsing.
If the script fails to recognize a time, it will throw an error with the invalid time string. This means it will cease all operation and the events after won't be processed
Please rerun the script everytime you wish to update the calendar, if past events have wrong details manually delete them from the calender first. 
