# Deskbird Booking Script

This Python script automates seat bookings on Deskbird and checks you in for today's bookings.

## Features

- **Automatic Booking**: The script tries to book your favorite seats for a specified date. If your first choice is unavailable, it moves on to the next.
- **Auto Check-In**: If you have a booking for today, it automatically checks you in.

## Requirements

- Python 3.7+
- The `requests` library

## Configuration

Create a `config.json` file in the same directory as the script. It should contain:
- `credentials.email`: Your Ekimetrics (Deskbird) account email
- `credentials.password`: Your Ekimetrics (Deskbird) account password
- `credentials.app_key`: The provided Deskbird API key
- `workspace_id`: The ID of the workspace you want to book
- `favorite_seats`: A dictionary of seat names, each with a `resource_id` and `zone_item_id`.
- `target_days`: List of days that you want the script to reserve. Possible values: ["Mon", "Tue", "Wed", "Thu", "Fri"]. When you are away for some time or want to cut off the script, simply remove days from target_days. 

The script will try each favorite seat in order until one is successfully booked.

## Running the Script

Make sure `config.json` is correctly filled out, then run the script using Python.

## Setting Up a Cron Job

You can schedule the script to run automatically at specific times (for example, between midnight and 9am) by setting up a cron job. Adjust the schedule, paths, and output redirection as needed.
Examples that runs at 00:00, 03:00, 06:00, 09:00 every day : 
```bash
crontab -e

0 0,3,6,9 * * * /usr/bin/python3 /path/to/deskbird_booking.py >> /path/to/deskbird_log.txt 2>&1
```


## Fetching resource_id and zone_item_id
To find the resource_id and zone_item_id for your favorite seats:

- Manually book some seats in your Deskbird interface.
- Run the script once (e.g., python3 deskbird_booking.py).
- The script will list your upcoming bookings, including resource_id and zone_item_id values in its output.
You can then simply add the values in your config.json

## Troubleshooting

- If you encounter authentication errors, double-check your credentials in `config.json`.
- Verify that the `workspace_id`, `resource_id`, and `zone_item_id` values are correct.
- Review any logs produced when using cron for more detailed error messages.
