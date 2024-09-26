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
