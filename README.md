# Simple WhatsApp Bot in Java for Beginners

This repository contains a basic WhatsApp bot written in Java, ideal for developers who are just starting out. The bot responds to various commands with text messages and images. With straightforward setup steps and detailed comments in the code, this bot is designed to help beginners understand API integration with WhatsApp.

## WhatsApp Bot Installation Guide (Java)

Follow these steps to set up and run the bot:

## Requirements
- **Java**: Version 17 or later  
  Check your version: `java -version`  
- **Maven**: Version 3.3.2 or later  
  Check your version: `mvn -version`

## Environment Variable Configuration
Set your **WHAPI_TOKEN** environment variable. This token authenticates your bot with the Whapi.Cloud API.  
Find the token in your [Whapi.Cloud](https://whapi.cloud) dashboard under API settings. Obtain an API token after [registration](https://panel.whapi.cloud/register). Here's a [step-by-step guide](https://support.whapi.cloud/help-desk/getting-started/getting-started#registration) on how to register and connect a number to get an API Token.

### Example:
###### For Mac/Linux:
```bash
export WHAPI_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
###### For Windows:
```bash
set WHAPI_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
![token](https://github.com/user-attachments/assets/98b624da-bf0e-474a-bce1-81384e103faa)

Alternatively, you can pass the token during runtime (details below).

## Video Tutorial:
For more detailed instructions on setup and configuration, you can watch our tutorial video on [YouTube](https://youtu.be/UnnQ2h0B4qg).

## Building and Running the Code

### Step 1: Build the Project

To compile and package the Java bot, use the Maven build tool. Run the following command from the root directory of your project:

```bash
mvn clean package
```
This will generate a `.jar` file located in the `target/` directory. The `.jar` file is the packaged application ready to execute.

### Step 2: Run the Bot

Once the `.jar` file is built, you can execute the bot using one of the two methods below:

#### Option 1: Using a Pre-configured Environment Variable

If the `WHAPI_TOKEN` environment variable is already set, you can run the bot with the following command:

```bash
java -jar ./target/whatsapp-bot-1.0.jar
```

This method is ideal if you’ve configured the token as a persistent environment variable.

#### Option 2: Passing the Token During Execution

Alternatively, you can pass the token directly as a command-line argument during runtime:

```bash
java -DWHAPI_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX -jar target/whatsapp-bot-1.0.jar
```
This approach is useful for one-off executions where the token is not stored as an environment variable.


## Webhook Configuration - Ngrok Setup

In order for the bot to receive incoming messages, you need to configure your server to accept return requests. For testing, a local server to access the internet with **ngrok** is ideal. Perform the following steps:

1. **Download ngrok**  
   If ngrok is not already installed, download it from the [official website](https://ngrok.com/download) and follow the installation instructions for your operating system.

2. **Start ngrok**  
   Run ngrok to forward requests to your local server (default port is 8080):
   ```bash
   ngrok http 8080
   ```
   After running this command, ngrok will generate a public HTTPS URL (e.g., https://random-string.ngrok.io). This URL will act as the endpoint for incoming messages and will be used to configure the webhook.
   
3. **Copy the URL and Set the Webhook in Whapi.Cloud**
   - Log in to your **Whapi.Cloud dashboard**.
   - Navigate to the **Channel Settings** section.
   - Paste the ngrok-generated URL and append `/webhook` to it. For example: `https://random-string.ngrok.io/webhook`.
   - Save the settings.

Your bot is now connected to the Whapi.Cloud API and can start receiving events and processing messages.

#### Main Logic

This is where the primary logic of the bot resides. It:
- Filters incoming messages (only non-outgoing messages are processed).
- Extracts the sender's phone number and the text content of the message.
- Uses a switch statement to respond with different messages or images based on the command received.

## Notes

### Environment Variables
If the `WHAPI_TOKEN` is not set as a persistent environment variable, you must pass it as a runtime argument using the `-DWHAPI_TOKEN` option when executing the bot. This ensures that the bot can authenticate with the Whapi.Cloud API.

### Port Configuration
Make sure your application listens on the same port specified when starting ngrok (default is `8080`). If you modify the port in your application, remember to adjust the ngrok command accordingly.

### Testing the Setup
After completing the setup, send a test message to the connected WhatsApp number to verify the bot's functionality. Monitor the application logs to ensure that the message is received and processed correctly.

### Troubleshooting Common Issues
If the bot does not respond as expected, follow these steps to diagnose and resolve the problem:

1. **Verify ngrok Status**  
   Ensure ngrok is running and the generated public URL is accessible. Test the URL in a browser to confirm it is forwarding requests correctly.

2. **Check Webhook Configuration**  
   Confirm that the webhook URL in the Whapi.Cloud dashboard matches the ngrok-generated URL with the `/webhook` endpoint appended. Double-check for typos or mismatches. Check to see if your webhook is receiving a reverse request by simulating a request to that address using endpoint: [https://whapi.readme.io/reference/webhooktest](https://whapi.readme.io/reference/webhooktest)

3. **Inspect Application Logs**  
   Review the logs generated by the bot for any errors or exceptions. Logs often provide valuable insights into configuration issues or runtime errors.

4. **Restart the Bot**  
   If changes were made to environment variables, ngrok, or the webhook configuration, restart the bot to ensure all updates are applied.

5. **Verify API Token**  
   Ensure the `WHAPI_TOKEN` is correctly set and matches the token provided in your Whapi.Cloud dashboard. Incorrect tokens will prevent authentication.

6. **Network Issues**  
   If the bot still fails to respond, check for network connectivity issues, such as firewalls or VPNs, that may block incoming requests.

7. **Make sure you're not writing yourself**  
   The bot will not be able to answer itself, so it is important that you text a number with the bot from a different number to test it.

---

By addressing these common challenges, you can ensure your WhatsApp bot runs smoothly and reliably. For additional support, refer to the [Whapi.Cloud documentation](https://whapi.cloud/docs) or reach out to [Whapi customer support team](https://whapi.cloud/support).

With your bot fully operational, you can now explore advanced features like automated messaging, media handling, and group management using the Whapi.Cloud API!

Happy coding!
