# impo-fullstack

The error `EADDRINUSE: address already in use :::8081` is indicating that the port `8081` is already occupied by another process on your system. This could happen if another instance of your app or some other service is already using the same port.

Here are steps to fix this issue:

### 1. **Terminate the Existing Process Using Port 8081**
   - Find the process running on port `8081` and terminate it:
     - On Windows:
       1. Run the following command in the command prompt or terminal to find the process ID (PID) using the port:
          ```bash
          netstat -ano | findstr :8081
          ```
       2. Note the PID from the output, and then terminate the process using:
          ```bash
          taskkill /PID <PID> /F
          ```
     - On Linux or macOS:
       1. Find the process:
          ```bash
          lsof -i :8081
          ```
       2. Kill the process:
          ```bash
          kill -9 <PID>
          ```

### 2. **Change the Port in Your Application**
   - If you don't want to terminate the existing process using the port, you can change the port used by your application. Open your `.env` file (or wherever the port is defined) and change the `PORT` variable:
     ```bash
     PORT=8082
     ```

   - You can also change the port directly in your code by passing a different port number in `app.listen()` in `index.js`:
     ```js
     app.listen(process.env.PORT || 8082, () => {
         console.log(`Backend Server Connected In The Port http://localhost:${process.env.PORT || 8082}`);
     });
     ```

### 3. **Check for Multiple Instances of Your App**
   - If you're developing and testing frequently, multiple instances of your application might be running in the background. Make sure only one instance is running by closing others or restarting your development environment.

### 4. **Use `rs` to Restart the App**
   - Nodemon allows you to restart the server by typing `rs` in the terminal. If you believe the port is not actually in use and this is a temporary glitch, you can try restarting:
     ```
     rs
     ```

After trying any of these solutions, your app should no longer face the "address already in use" issue.


In the output you provided:

```
  TCP    0.0.0.0:8081           0.0.0.0:0              LISTENING       6732
  TCP    [::]:8081              [::]:0                 LISTENING       6732
```

The PID (Process ID) is **6732**.

To terminate this process, you can use the following command in the command prompt:

```bash
taskkill /PID 6732 /F
```

This command will forcefully terminate the process that is currently using port `8081`. After doing this, you should be able to run your Node.js application again without encountering the `EADDRINUSE` error.

To uninstall an npm package from the command line (cmd), you can use the following command:

```bash
npm uninstall <package-name>
```

For example, to uninstall a package called `lodash`, you would run:

```bash
npm uninstall lodash
```

### Additional Options:
- To uninstall a package and remove it from the `dependencies` in your `package.json`:
  ```bash
  npm uninstall <package-name> --save
  ```

- To uninstall a package from `devDependencies`:
  ```bash
  npm uninstall <package-name> --save-dev
  ```

- If you're working globally, and you want to uninstall a globally installed package, you can add the `-g` flag:
  ```bash
  npm uninstall -g <package-name>
  ```

This will remove the specified npm package from your project or globally, depending on the command used.

# This Is For Full Stack Ecommerce Project To Send Mail For Forget password and what to need to change in your sender mail account. IT IS VERY IMPORTANT
The error message you’re seeing (`Invalid login: 534-5.7.9 Application-specific password required`) is related to Google’s security measures, which prevent unauthorized access to Gmail SMTP by requiring an "App Password" for third-party applications. Here’s how to resolve this issue:

1. **Enable Two-Factor Authentication (2FA)** for your Google account if you haven't already:
   - Go to [Google Account Security](https://myaccount.google.com/security).
   - Under the "Signing in to Google" section, enable **2-Step Verification**.

2. **Generate an App Password** specifically for your application:
   - Once 2FA is enabled, go to [App Passwords](https://myaccount.google.com/apppasswords).
   - Select an "App" (like Mail) and a "Device" (like Other).
   - Enter a name, such as "NodeJS ECommerce App," and click "Generate."
   - Google will provide you with a 16-character password.

3. **Update Your `.env` File**:
   - Replace the `SMTP_MAIL_PASSWORD` in your `.env` file with the newly generated App Password.

   ```env
   SMTP_MAIL = "kumarsahuatish@gmail.com"
   SMTP_MAIL_PASSWORD = "your-app-password-here"
   ```

4. **Restart Your Node Server** after making the changes to ensure it picks up the new environment variables.

### Why This Works
Google blocks regular passwords in SMTP connections if 2FA is enabled for security reasons. The App Password bypasses this restriction while still protecting your account, allowing your app to access the Gmail SMTP server securely.

After following these steps, try sending the forget password email again, and it should work without any issues. Let me know if you encounter any more problems!
