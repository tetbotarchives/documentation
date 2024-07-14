# User Guide: Adding Commands to Your Telegram Bot

Welcome to the detailed guide on adding new commands to your Telegram bot using our service. This guide will walk you through the steps required to add, remove, and list commands for your bot.

## Adding a New Command

To add a new command to your bot, use the `/addcmd` command followed by the command name and the code to be executed. Below is a step-by-step guide on how to do this.

### Step-by-Step Guide

1. **Open your Telegram chat with the bot.**
2. **Type the following command:**
   ```
   /addcmd command_name code
   ```

   - `command_name`: Replace this with the name you want to give to your new command.
   - `code`: Replace this with the Python code that you want to execute when the command is called.

### Example

Let’s say you want to create a command called `/greet` that sends a greeting message.

**Command:**
```
/addcmd greet safe_reply(update, "Hello! How can I assist you today?")
```

When you type `/greet` in the chat, the bot will reply with "Hello! How can I assist you today?".

### Notes

- Ensure the command name is unique and does not conflict with existing commands.
- The code should only use the functions provided (`safe_get` and `safe_reply`) to ensure security and proper execution.

## Removing an Existing Command

To remove an existing command from your bot, use the `/removecmd` command followed by the command name.

### Step-by-Step Guide

1. **Open your Telegram chat with the bot.**
2. **Type the following command:**
   ```
   /removecmd command_name
   ```

   - `command_name`: Replace this with the name of the command you want to remove.

### Example

If you want to remove the command `/greet`, type the following:

**Command:**
```
/removecmd greet
```

This will remove the `/greet` command from your bot.

## Listing All Active Commands

To list all currently active commands, use the `/listcmds` command.

### Step-by-Step Guide

1. **Open your Telegram chat with the bot.**
2. **Type the following command:**
   ```
   /listcmds
   ```

The bot will reply with a list of all active commands.

### Example

**Command:**
```
/listcmds
```

The bot will respond with something like:
```
Active temporary commands:
/greet
/another_command
```

## Safety and Security

To ensure the safety and security of your bot, only specific functions are allowed in the command code. These functions are:

- **`safe_get(url)`**: Fetches data from a URL safely, handling errors and timeouts.
- **`safe_reply(update, text)`**: Sends a reply to the user, ensuring the message length does not exceed Telegram's limit.

### Example of Safe Code

Here is an example of safe code that can be used with the `/addcmd` command:

```
safe_reply(update, "This is a safe reply.")
```

## Summary

- **Add a Command:** `/addcmd command_name code`
- **Remove a Command:** `/removecmd command_name`
- **List Commands:** `/listcmds`

## Advanced Example: Adding More Complex Commands

Now that you understand the basics of adding, removing, and listing commands, let's explore a more complex example. This will demonstrate how to use the available functions (`safe_get` and `safe_reply`) to create a more functional command.

### Complex Example: Fetching Data from an API

Let's create a command called `/weather` that fetches weather data from an API and sends the weather information to the user.

### Step-by-Step Guide

1. **Open your Telegram chat with the bot.**
2. **Type the following command:**
   ```
   /addcmd weather
   code
   ```

   - `weather`: This is the name of the new command.
   - `code`: This is the Python code to fetch weather data and send it to the user.

### Code Example

To keep things simple, let's assume you have an API endpoint `https://api.example.com/weather` that returns weather data in JSON format.

**Command:**
```
/addcmd weather
safe_reply(update, "Fetching weather data...")
data = safe_get("https://api.example.com/weather")
if "Error" not in data:
    weather_info = f"Temperature: {data['temp']}°C\nCondition: {data['condition']}"
    safe_reply(update, weather_info)
else:
    safe_reply(update, "Failed to fetch weather data.")
```

### Breakdown of the Code

1. **Initial Response:**
   ```python
   safe_reply(update, "Fetching weather data...")
   ```
   - This line sends a message to the user indicating that the bot is fetching weather data.

2. **Fetching Data:**
   ```python
   data = safe_get("https://api.example.com/weather")
   ```
   - This line uses the `safe_get` function to fetch data from the weather API. The data is stored in the `data` variable.

3. **Processing the Data:**
   ```python
   if "Error" not in data:
       weather_info = f"Temperature: {data['temp']}°C\nCondition: {data['condition']}"
       safe_reply(update, weather_info)
   else:
       safe_reply(update, "Failed to fetch weather data.")
   ```
   - This block checks if the fetched data contains an error message. If not, it formats the weather information and sends it to the user. If there is an error, it sends a failure message to the user.

### Result

When a user types `/weather` in the chat, the bot will:
1. Send "Fetching weather data..."
2. Fetch data from the API.
3. If successful, send the weather information.
4. If there's an error, notify the user of the failure.

## Another Example: Combining Multiple Functions

Let's create a command called `/crypto` that fetches cryptocurrency prices from an API and sends the prices to the user.

### Step-by-Step Guide

1. **Open your Telegram chat with the bot.**
2. **Type the following command:**
   ```
   /addcmd crypto
   code
   ```

   - `crypto`: This is the name of the new command.
   - `code`: This is the Python code to fetch cryptocurrency prices and send them to the user.

### Code Example

Assume you have an API endpoint `https://api.example.com/crypto` that returns cryptocurrency prices in JSON format.

**Command:**
```
/addcmd crypto
safe_reply(update, "Fetching cryptocurrency prices...")
data = safe_get("https://api.example.com/crypto")
if "Error" not in data:
    crypto_info = "\n".join([f"{coin['name']}: ${coin['price']}" for coin in data])
    safe_reply(update, crypto_info)
else:
    safe_reply(update, "Failed to fetch cryptocurrency prices.")
```

### Breakdown of the Code

1. **Initial Response:**
   ```python
   safe_reply(update, "Fetching cryptocurrency prices...")
   ```
   - This line sends a message to the user indicating that the bot is fetching cryptocurrency prices.

2. **Fetching Data:**
   ```python
   data = safe_get("https://api.example.com/crypto")
   ```
   - This line uses the `safe_get` function to fetch data from the cryptocurrency API. The data is stored in the `data` variable.

3. **Processing the Data:**
   ```python
   if "Error" not in data:
       crypto_info = "\n".join([f"{coin['name']}: ${coin['price']}" for coin in data])
       safe_reply(update, crypto_info)
   else:
       safe_reply(update, "Failed to fetch cryptocurrency prices.")
   ```
   - This block checks if the fetched data contains an error message. If not, it formats the cryptocurrency prices and sends them to the user. If there is an error, it sends a failure message to the user.

### Result

When a user types `/crypto` in the chat, the bot will:
1. Send "Fetching cryptocurrency prices..."
2. Fetch data from the API.
3. If successful, send the cryptocurrency prices.
4. If there's an error, notify the user of the failure.

## Summary

- **Add a Command:** `/addcmd command_name code`
  - **Example:**
    ```
    /addcmd greet safe_reply(update, "Hello! How can I assist you today?")
    ```
- **Remove a Command:** `/removecmd command_name`
  - **Example:**
    ```
    /removecmd greet
    ```
- **List Commands:** `/listcmds`
  - **Example:**
    ```
    /listcmds
    ```

These examples demonstrate how to create more complex commands using the available functions. By following these steps, you can extend your bot's functionality while maintaining safety and security. If you have any questions or need further assistance, please contact our me.





