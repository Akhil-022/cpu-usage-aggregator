This project aggregates CPU usage data for users on a Unix-like system and sends the metrics to specified Telegram chats/channels.

Installation
Clone the repository:

git clone https://github.com/Shra1V32/cpu-usage-aggregator.git
cd cpu-usage-aggregator
Install the required dependencies:

sudo pip install -r requirements.txt
It's necessary to use sudo to install the dependencies as the script needs to be run with root privileges.

Create a .env file in the project directory with the following content:

API_ID = <your_api_id>
API_HASH = "<your_api_hash>"
BOT_TOKEN = "<your_bot_token>"
CHAT_ID = <your_chat_id_1>,<your_chat_id_2>
Replace the placeholders with your own values.

The CHAT_ID field can contain multiple chat IDs separated by commas. The API_ID and API_HASH fields are required to authenticate the bot with the Telegram API. You can obtain these values by creating a new application on the Telegram Apps page. The BOT_TOKEN field is required to authenticate the bot with the Telegram API. You can obtain this value by creating a new bot using the BotFather bot on Telegram.

Usage
Ensure that the sa command is available on your system. This command is typically part of the acct package, which can be installed using:

sudo apt-get install acct
The sa command is used to generate CPU usage logs for users. For other distributions, you can install the acct package using the package manager specific to that distribution.

Run the script:

sudo python main.py
The script must be run with root privileges to access the CPU usage logs.

Scheduled Execution
You can schedule the script to run at regular intervals using cron. To edit the cron jobs, run:

sudo crontab -e
sudo is neccessary to edit the cron jobs as the script needs to be run with root privileges.

Add the following line to the cron file to run the script for every six hours:

0 */6 * * * /usr/bin/python3 /path/to/cpu-usage-aggregator/main.py
Replace /path/to/cpu-usage-aggregator with the path to the project directory.

Save and exit the editor to apply the changes.

How It Works
The script reads the list of users from /etc/passwd and filters out the users specified in the IGNORANT_USERS list.

It saves the CPU usage logs by running the sa -u command and storing the output in /var/log/user_cpu_usage.

The aggregate_cpu_usage function processes the logs to calculate the total CPU time used by each user.

The send_metrics function sends the aggregated CPU usage data to the specified Telegram chats.

Functions
save_logs(): Saves the CPU usage logs to a file.
parse_log(file_path): Parses a log file to extract CPU usage data.
aggregate_cpu_usage(log_dir): Aggregates CPU usage data from log files.
send_metrics(): Sends the aggregated CPU usage data to Telegram chats.
License
This project is licensed under the MIT License. See the LICENSE file for details
